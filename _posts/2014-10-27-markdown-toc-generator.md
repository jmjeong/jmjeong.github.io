---
layout: post
title: Markdown toc generator
modified: 
category: python
tags: python
---

Markdow 문서에서 목차를 만들어내는 프로그램


```sh
usage: toc.py [-h] [-d DEPTH] [-c] [-i INDENT] [-f FORMAT] filename

positional arguments:
  filename

optional arguments:
  -h, --help            show this help message and exit
  -d DEPTH, --depth DEPTH
                        Start section number
  -c, --clipboard       Copy output to clipboard
  -i INDENT, --indent INDENT
                        Indent size
  -f FORMAT, --format FORMAT
                        ex) DDD* - D:1. d:1.1. *:* a:a. A:A. H:가. h:ㄱ.
```

`-d` option은 무시할 subsection, `-c` option을 주면 내용이 clipboard에 복사된다.
`-i` option은 section이 표시될 때 사용될 indent size이고, `-f` option은 제목의 format을 지정한다.

```
jmjeong$ ./toc.py mtest.md
1. A
    1. Aa
        * aa
        * ab
    2. Ab
2. B
    1. Ba
        * ba
        * bb
    2. Bb
    3. Bc
3. C
    1. Ca
        * ca
jmjeong$ ./toc.py -f ADh mtest.md
A. A
    1. Aa
        ㄱ. aa
        ㄴ. ab
    2. Ab
B. B
    1. Ba
        ㄱ. ba
        ㄴ. bb
    2. Bb
    3. Bc
C. C
    1. Ca
        ㄱ. ca
jmjeong$ ./toc.py -f Add mtest.md
A. A
    1.1. Aa
        1.1.1. aa
        1.1.2. ab
    1.2. Ab
B. B
    2.1. Ba
        2.1.1. ba
        2.1.2. bb
    2.2. Bb
    2.3. Bc
C. C
    3.1. Ca
        3.1.1. ca
jmjeong$ ./toc.py -f Hd* mtest.md
가. A
    1.1. Aa
        * aa
        * ab
    1.2. Ab
나. B
    2.1. Ba
        * ba
        * bb
    2.2. Bb
    2.3. Bc
다. C
    3.1. Ca
        * ca		
```

--- 

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# markdown toc generator, v1.8
#
# Jaemok Jeong, 2014/10/27

from AppKit import NSPasteboard, NSArray
import re
import argparse

headRe = re.compile(r"(#+)\s*([^#]*)")

import sys
reload(sys)
sys.setdefaultencoding('utf-8')

def sendToClipboard(content):
    pb = NSPasteboard.generalPasteboard()
    pb.clearContents()
    c = NSArray.arrayWithObject_(content)
    pb.writeObjects_(c)


def generateSectionNum(format, depth, pos, sectionCount):
    # print format, depth, pos, sectionCount
    ganadara = u'가나다라마바사아자차카타파하'
    gndr = u'ㄱㄴㄷㄹㅁㅂㅅㅇㅈㅊㅋㅌㅍㅎ'
    try:
        currentFormat = format[pos-depth]
    except IndexError:
        currentFormat = 'D'

    if currentFormat == 'd':
        return ".".join([str(s) for s in sectionCount if s != 0])[(depth-1)*2:]+"."
    elif currentFormat == '*':
        return "*"
    elif currentFormat == 'A':
        return chr(ord('A')+sectionCount[pos-1]-1)+"."
    elif currentFormat == 'a':
        return chr(ord('a')+sectionCount[pos-1]-1)+"."
    elif currentFormat == 'H':
        return ganadara[sectionCount[pos-1]-1]+"."
    elif currentFormat == 'h':
        return gndr[sectionCount[pos-1]-1]+"."
    else:
        return str(sectionCount[pos-1])+"."

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("-d", "--depth", help="Start section number", type=int, default=2)
    parser.add_argument("-c", "--clipboard", help="Copy output to clipboard", dest='clipboard', action='store_true')
    parser.add_argument("-i", "--indent", help="Indent size", type=int, default=4)
    parser.add_argument("-f", "--format", help="ex) DDD* - D:1. d:1.1. *:* a:a. A:A. H:가. h:ㄱ.", default="DD**")
    parser.add_argument('filename')

    args = parser.parse_args()

    sectionCount = [0,0,0,0,0]
    currentPos = 0
    toc = ""

    with open(args.filename, "r") as f:
        for line in f.readlines():
            l = line.strip()
            if l.startswith("#"):
                m = headRe.match(l)
                c = len(m.group(1))
                if (c < args.depth):
                    continue
                if c == currentPos:
                    sectionCount[c-1] += 1
                elif c > currentPos:
                    for i in range(currentPos,c):
                        sectionCount[i] = 1
                    currentPos = c
                else:
                    sectionCount[c-1] += 1
                    for i in range(c,currentPos):
                        sectionCount[i] = 0
                    currentPos = c

                sec = generateSectionNum(args.format, args.depth, currentPos, sectionCount)
                spaces = " "*(currentPos-args.depth)*args.indent
                newsec = spaces + "%s %s\n" % (sec, m.group(2))
                print newsec.rstrip().encode('utf-8')
                toc += newsec
    if args.clipboard:
        sendToClipboard(toc)
    
if __name__ == '__main__':
    main()
```


