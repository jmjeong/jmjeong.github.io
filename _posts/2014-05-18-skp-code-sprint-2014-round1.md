---
layout: single
title: 2014 SKP Code Sprint Round1
description: 
category: python
tags: programming python
image:
  teaser: t-python.jpg
---

2014 SKP Code Sprint Round 1에 참가. 1 Round는 11위, 최종 라운드는 27위. 주말에 다른
일정이 있어서 첫번째 round 소스만 제출하고 더 이상 upgrade는 진행하지 않았음. Python이라 10초 시간
limit 내에서 최적화하기 쉽지 않을 것 같기도 함.

- [문제 Link](https://codesprint.skplanet.com/2014/participation/round1_intro.htm)
- [제출 답안](http://cl.ly/0K090l092p47/skp-code-sprint-round1.zip)

# 알고리즘

mixedbulgogistew 단어가 조합되는 경우의 수는 `2**15` 이다. 각 문자 사이가 단어의 구별자가 될지 말지에
따라 2**(n-1)의 경우의 수가 생긴다.  각각 나눠진 word 마다 corpus에서 나오는 확률을 계산한다. 즉
`P(m)*p(i)*P(x)*...*P(w)`,..,`P(mixed)*P(bulgogi)*P(stew)`등의 조합 중에서 Pw 값이 제일 높은 pair를
찾아낸다.train.py 프로그램을 통해 corpus와 train.qry 정답으로부터 각 단어가 나타나는 확률을 계산하여
json 형태의 dictionary로 저장한다. tester.py 에서는 이 json을 읽어서 Pw를 참조한다. 

segment 함수는 재귀호출을 통해 구현하되, 중간 계산 결과는 dictionary에 저장하여 속도를 높인다.

참고문헌 : chapter 14. "Natural Language Corpus Data" from the book "Beautiful Data" (Segaran and Hammerbacher, 2009)

# 코드

train.py 에서 train.txt와 train.qry를 읽어서 각 단어별 출현 빈도를 계산하여 저장한다. train.qry에
정답이 들어 있기 때문에 가중치를 두어 계산한다.

`train_model['1']`에는 1번 모델, `train_model['2']`에는 2번 모델, `train_model['3']`에는 3번 모델에
대한 각각의 단어 확률이 저장되어 있다. 

segment('word')가 호출되면 다음과 같은  recursive call로 처리한다.

  - ['w'] + segment('ord')
  - ['wo'] + segment('rd')
  - ['wor'] + segment('d')
  
계산 시간을 줄이기 위해 recursive call의 중간 단계에 나오는 공통 결과를 dictionary로 저장한다.
이렇게 만들어진 pair 중에서 Pwords(Pw(1)*Pw(2)*...*Pw(n))의 값이 가장 높은 list를 결과로 반환한다. 

## train.py

- model 1 : train.qry의 정답 자료에 corpusN/answerN 가중치 부여 
- model 2 : train.qry의 정답 자료에 corpus에서 제일 많이 나온 단어수 가중치 부여 
- model 3 : train.qry의 정답 자료에 corpusN 가중치 부여 

- train.qry로 테스트했을 때 오답 수 (model1 : 709, model2: 151, model3: 143)

# 실행 환경

- MacOS 10.9.2
- Python version 2.7.5

# 실행 방법

- src directory에서 수행
- train.py (학습방법)
   $ python train.py [../res/train.txt] [../res/train.qry] [../oth/train.model]
     - train.txt train.qry를 읽어서 결과로 train.model을 만들어 저장한다. 
- tester.py (실행방법)
   $ python tester.py [1,2,3] [../res/query.txt] [../ans/] [../oth/train.model]
     - 첫번째 인자 : 1,2,3 모델 중에서 어떤 것을 사용할지 지정 (없으면 3)
	 - 두번째 인자 : query data [../res/query.txt] default로 사용
	 - 세번째 인자 : output을 저장할 directory [../ans/] 저장 파일명은 두번째인자.ans.모델
	 - 네번째 인자 : train.py에서 저장한 model [../oth/train.model] default로 사용 
      
# 실행 예 

	jmjeong/src $ python train.py 
	Make model from '../res/train.txt' and '../res/train.qry'

	- corpus (wordN,corpusN) = 30229, 1258707
	- answer (wordN,corpusN) = 5954, 26106

	Writing '../oth/train.model'
	jmjeong/src $ python tester.py 1
	Using model-1 in ../oth/train.model
	Reading ../res/test.qry
	Writing ../ans/test.ans.1
	Elapsed time: 4s, Total cnt: 10000
	jmjeong/src $ python tester.py 2
	Using model-2 in ../oth/train.model
	Reading ../res/test.qry
	Writing ../ans/test.ans.2
	Elapsed time: 4.2s, Total cnt: 10000
	jmjeong/src $ python tester.py 3
	Using model-3 in ../oth/train.model
	Reading ../res/test.qry
	Writing ../ans/test.ans.3
	Elapsed time: 4.3s, Total cnt: 10000

# Source

## train.py

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# corpus trainer, v1.0
#
# Jaemok Jeong(jmjeong@gmail.com), 2014/05/14

import re
import collections
import json
import sys

# train.txt와 train.qry로부터 word별 확률 model을 만든다. 
#
# model 1 : train.qry의 정답 자료에 corpusN/answerN 가중치 부여 
# model 2 : train.qry의 정답 자료에 corpus에서 제일 많이 나온 단어수 가중치 부여 
# model 3 : train.qry의 정답 자료에 corpusN 가중치 부여 
#
# 결과는 dictionary 형태로 train.model로 저장한다. 

def train():
    corpus_fname = len(sys.argv)>1 and sys.argv[1] or "../res/train.txt"
    query_fname = len(sys.argv)>2 and sys.argv[2] or "../res/train.qry"
    model_fname = len(sys.argv)>3 and sys.argv[3] or "../oth/train.model"

    print "Make model from '%s' and '%s'\n" % (corpus_fname, query_fname)

    try:
        fcorpus = open(corpus_fname, "r")
        fquery = open(query_fname, "r")
    except IOError:
        print "File open Error"
        sys.exit(1)

    # train.txt 파일로부터 단어의 빈도 조사
    dict_corpus = collections.Counter()
    for line in fcorpus:
        words = re.findall(r'\w+',line.strip().lower())
        
        for w in words:  # single corpus
            dict_corpus[w] += 1
    corpusN = float(sum(dict_corpus.itervalues()))

    # train.qry 파일로부터 정답의 빈도 조사
    dict_answer = collections.Counter()
    for line in fquery:
        (ques,ans) = line.strip().lower().split('\t')
        words = re.findall(r'\w+',ans)
        
        for w in words:
            dict_answer[w] += 1
    answerN = float(sum(dict_answer.itervalues()))

    print "- corpus (wordN,corpusN) = %d, %d" % (len(dict_corpus),corpusN)
    print "- answer (wordN,corpusN) = %d, %d" % (len(dict_answer),answerN)
    
    # print "* most common 7 (corpus)"
    # print " ", dict_corpus.most_common(7)
    # print "* most common 7 (answer)"
    # print " ", dict_answer.most_common(7)
    
    # 1. train.qry의 정답 자료에 corpusN/answerN 가중치 부여
    # 2. train.qry의 정답 자료에 corpus에서 제일 많이 나온 단어수 가중치 부여 
    # 3. train.qry의 정답 자료에 corpusN 가중치 부여
    models = []
    for mod in (corpusN/answerN, dict_corpus.most_common(1)[0][1]+1,corpusN):
        d = {}
        for key in set(dict_corpus.keys()+dict_answer.keys()):
            val = 0
            if key in dict_corpus:
                val += dict_corpus[key]
            if key in dict_answer:
                val += dict_answer[key]*mod
            d[key] = val / (corpusN+answerN*mod)
        d['$n'] = corpusN+answerN*mod
        models.append(d)

    train_model = { '1': models[0],'2': models[1], '3': models[2] }
    
    with open(model_fname, "w") as f:
        f.write(json.dumps(train_model))

    print "\nWriting '%s'" % model_fname

if __name__ == '__main__':
    train()
```

## tester.py

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# tester.py, v1.0
#
# Jaemok Jeong(jmjeong@gmail.com), 2014/05/14

# Reference :
#
#  "Natural Language Corpus Data" from the book "Beautiful Data" (Segaran and Hammerbacher, 2009)
#   http://oreilly.com/catalog/9780596157111/

import operator
import json
import time
import sys
import os

MAX_CORPUS = 20

def Pw(key):
    """각 단어의 빈도 확률
    저장된 dict_model의 확률 table 값을 참조:"""
    if key in dict_model: return dict_model[key]
    else: return 10./(dict_model['$n'] * 10**len(key))

def memoize(f):
  class memodict(dict):
      __slots__ = ()
      def __missing__(self, key):
          self[key] = ret = f(key)
          return ret
  return memodict().__getitem__

@memoize
def segment(text):
    """가장 최적으로 잘려진 단어 리스트를 반환
    Recursion을 이용하여 단어를 분리 후, 각 list의 각 단어 확률의 곱이 최대가 되는 Pair를 결과로 반환 
    중복계산을 막기 위해 memoize decorator를 이용하여 중간 결과를 dictionary에 저장
    """
    if not text: return []
    cs = ([f]+segment(r) for f,r in [(text[:i+1], text[i+1:]) for i in range(min(len(text), MAX_CORPUS))])
    return max(cs, key=lambda words: reduce(operator.mul, (Pw(w) for w in words)))

if __name__ == '__main__':
    global dict_model

    start = time.clock()

    model = len(sys.argv)>1 and sys.argv[1] or '3'
    ifname = len(sys.argv)>2 and sys.argv[2] or '../res/test.qry'
    outdir = len(sys.argv)>3 and sys.argv[3] or '../ans'
    modelname = len(sys.argv)>4 and sys.argv[4] or '../oth/train.model'

    ofname = os.path.join(outdir, os.path.splitext(os.path.basename(ifname))[0]+".ans."+model)
    train_model = json.loads(open(modelname, 'r').read())
    print "Using model-%s in %s" % (model, modelname)
    print "Reading %s" % ifname
    
    dict_model = train_model[model]

    of = open(ofname,'w')
    cnt = 0
    with open(ifname, 'r') as f:
        for line in f:
            # (q,a) = line.strip().split('\t')
            # ans = " ".join(segment(q))
            ans = " ".join(segment(line.strip()))
            cnt += 1
            # if ans != a:
            #     print q, ":", "[", a, "]", ans
            #     cnt += 1
            of.write(ans+"\n")
    end = time.clock()
    of.close()
    print "Writing %s" % ofname
    print "Elapsed time: %.2gs, Total cnt: %d" % ((end-start), cnt)
```
