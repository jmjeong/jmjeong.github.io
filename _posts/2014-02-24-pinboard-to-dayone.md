---
layout: post
title: 'pinboard to dayone'
description: "매일 Pinboard 저장된 bookmark를 dayone에 archive하는 script"
tags: python pinboard
---

매일 pinboard에 bookmark한 link를 day one에 markdown 형식으로 자동으로 옮기기 위한 스크립트이다. 

![](http://farm3.staticflickr.com/2860/12746368525_3abc625962.jpg)

#### 설치 

- [Day One Tools](https://dayone.zendesk.com/hc/en-us/articles/200258954-Day-One-Tools) ([Download](http://dayoneapp.com/downloads/dayone-cli.pkg))
- PINBOARD_TOKEN 설정 : [Get it](https://pinboard.in/settings/password)
	- username:TOKEN 형식으로 설정하면 된다. 
- 프로그램을 cron job에 등록 
	- 5 0 * * * python /path/to/pinboard-to-dayone.py > /dev/null 2>&1

#### 프로그램 소스 (pinboard-to-dayone.py)

<script src="https://gist.github.com/jmjeong/5dbe5c45bfe0f79d3a13.js"></script>

####  참고 

- [Slogger](http://ttscoff.github.com/Slogger/)
