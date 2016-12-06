---
layout: post
title: "PlanBe QuickAdd 사용법"
description: ""
category: ios
tags: planbe ios
---


PlanBe의 QuickAdd는 빠른 일정 입력을 돕기 위해 만들어졌습니다. 기본적인 문법은 다음과 같습니다. 

{% highlight console %}
[날짜 및 시간] 제목 [@장소] [/캘린더] [!]
{% endhighlight %}

문법으로 설명하면 복잡하니 간단한 예를 들어 설명을 하겠습니다. 
아래는 일정에 대해서 예를 들었으나 날짜와 시간 지정하는 항목은 할 일에 대해서도 동일하게 적용됩니다. 

### 사용 예제

- `1/3 meeting`  1월 3일 종일 일정으로 만들어집니다. 
- `1/5 12 lunch`  1월 5일 12시 일정으로 만들어집니다. 
- `830p book` : 선택된 날짜 오후 8시 30분에 book이라는 일정이 만들어집니다.  a/p로 오전 오후를 지정할 수 있습니다. 
- `1/10-13 conference`  1월 10일부터 13일까지 conference라는 일정을 등록합니다. 
- `next mon meeting`  다음주 월요일 meeting 일정이 만들어집니다. 
- `130-2:30` : 선택된 날짜의 1시 30분부터 2시 30분까지 일정으로 만들어집니다. 
- `14-15 meeting`  오후 2시부터 오후 3시까지 meeting 일정이 만들어집니다. 
- `n PlanBe Tip 쓰기 /log`  현재시간에 Log 라는 캘린더에 'PlanBe Tip 쓰기' 라는 일정을 기록합니다.  
- `\- 음반사기`  할 일 항목에 '마감일 지정'이 안 된 todo를 만들기 위해서는 시작을 -로 입력하면 됩니다. 
- `1230 meeting`  12시 30분 meeting 일정
- `1420-1530 meeting`  오후 2시 20분부터 3시 30분까지의 meeting 일정
- `13 meeting`  오후 1시 미팅 일정
- `1/14 130p-140p meeting`  1월 14일 오후 1시 30분부터 1시 40분까지의 meeting 일정
- `+1 meeting`  1분 뒤의 meeting 일정 
- `+1h lost cities`  1시간 뒤 'lost cities' 일정 등록 
- `+1d write report`  내일 날짜에 write report 일정 등록
- `+1w buy present`  1주일 뒤 날짜에 buy present 일정 등록
