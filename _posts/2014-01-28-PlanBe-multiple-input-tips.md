---
layout: post
title: "PlanBe와 x-callback-url을 이용하여 여러 일정/할 일 등록"
category: ios
tags: planbe ios
---

PlanBe와 x-callback-url을 이용한 할 일 여러개 등록하는 Tip 입니다. 

### 다수의 할 일을 한꺼번에 미리알림에 등록하기

	namuplanbe://x-callback-url/parse?title=[[draft]]&type=t&x-source=Drafts&prompt=y&x-success={{drafts://}}

- Action 자동등록 URL : [링크](drafts://x-callback-url/import_action?type=URL&name=PlanBe%20Reminder%20%28multi%29&url=namuplanbe%3A%2F%2Fx-callback-url%2Fparse%3Ftitle%3D%5B%5Bdraft%5D%5D%26type%3Dt%26x-source%3DDrafts%26prompt%3Dy%26x-success%3D%7B%7Bdrafts%3A%2F%2F%7D%7D)

![Draft](http://farm3.staticflickr.com/2886/12182434645_c5fe8348ba.jpg)
![PlanBe](http://farm3.staticflickr.com/2816/12183315166_79aea79ebb.jpg)

- **-** 로 시작하는 라인은 [마감일 없음] 일정입니다
- 2/1 일 처럼 QuickAdd 에 쓰이는 여러 날짜/시간 지정 항목을 쓸 수 있습니다
- +1w 오늘로부터 1주일 뒤 할 일로 등록합니다. +2w, +1m을 통해 각각 2주 뒤, 한달 뒤 할 일을 등록할 수 있습니다. 

<iframe width="620" height="515" src="//www.youtube.com/embed/Xfuz_m54X9E" frameborder="0" allowfullscreen></iframe>

Lite 버전 사용하시는 분은 namuplanbelite 로 변경하면 동작합니다. 
