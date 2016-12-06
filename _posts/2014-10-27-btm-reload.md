---
layout: post
title: Back To The Mac RSS reloader
description: 
category: mac
tags:
image:
  teaser: t-python.jpg

---

- [https://github.com/jmjeong/alfred-extension/tree/master/backtothemac](https://github.com/jmjeong/alfred-extension/tree/master/backtothemac)

alfred2 [back to the mac] 스크립트를 수행할 때, 데이타가 1시간 전이면 server로부터 rss를 다시
읽어오도록 되어 있다. 수행할 때마다 delay하는 것이 번거로워, cron job으로 수행할 script를 만들었다. 

`btm-reload.py`와 `feedparser.py`를 같은 directory에 두고
`btm-reload.py`를 cron job에 등록하면 15분마다 읽어서 cache를 하게 된다. 


{% highlight sh %}
*/15 * * * * /Users/jmjeong/Dropbox/bin/btm-reload.py > /dev/null 2>&1
{% endhighlight %}

- [btm-reload.py](https://gist.github.com/jmjeong/aaf54290bd4604c07036)
- [feedparser.py](https://gist.github.com/jmjeong/2a7a814012f202709f4d)
