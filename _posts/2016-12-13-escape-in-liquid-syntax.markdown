---
title: Jekyll에서 liquid warning 처리
layout: post
tags: jekyll
---

{% raw %}
Jekyll 에서 사용되는 liquid가 `{{`와 }}`를 escape 문자로 사용합니다. 
문서에 {{, }} 가 들어 있는 경우 jekyll engine이 경고 메시지를 출력하고,
{{ ... }}  사이에 있는 내용은 무시됩니다. 

문서에는  `x-success={{drafts://}}` 라는 문장이 들어 있습니다. 

```
Liquid Warning: Liquid syntax error (line 20): Unexpected character / in "{{drafts://}}" in 
 <path>/2014-04-02-happydays-x-callback-url.md
```

임시적으로 해당 내용을 liquid parsing을 하지 않기 위해서는 문장 앞뒤로 다음과 같은 tag를 추가해 주면
warning과 출력 문제를 해결할 수 있습니다. 

![](http://d.jmjeong.com/K4a5+)

{% endraw %}