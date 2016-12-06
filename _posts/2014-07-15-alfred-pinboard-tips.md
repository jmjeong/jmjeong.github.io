---
layout: post
title: alfred-pinboard 팁 모음
description: 
category: 
tags: pinboard alfred
image:
 teaser: t-alfred-pinboard-2.jpg
---

### alfred-pinboard links

- [Github alfred-pinboard Project 페이지](https://github.com/jmjeong/alfred-extension/tree/master/alfred-pinboard)
- [jmjeong.com의 페이지]({% post_url 2014-05-26-alfred-pinboard-v2 %})

### Hot key 설정

처음에 workflow를 import 하면 hotkey가 설정되어 있지 않습니다. 
alfred에서 보안 이슈로 모든 hotkey를 초기화합니다.

다음은 제가 설정해서 사용하고 있는 hotkey 목록입니다.  Hotkey 설정은 비어 있는 Hotkey란을 더블클릭
후에 키를 지정하면 됩니다.

pinboard 내용을 보고 싶은 경우에는 ctl-shift-cmd-p (pinboard) 를 누르고, 마지막에 참조했던 bookmark는
ctl-shift-cmd-l (last bookmark)를 누르면 바로 창이 뜹니다.

- ctl-shift-cmd-p : launch **pba** 
- ctl-shift-cmd-c : launch **pba #** 
- ctl-shift-cmd-n : launch **pbnote**
- ctl-shift-cmd-s : launch **pbs**
- ctl-shift-cmd-h : launch **pbhis**
- ctl-shift-cmd-l : launch **pblog**

![alfred-pinboard-tips](https://farm3.staticflickr.com/2940/14656379314_ce8d3c48a5.jpg)

### Tag 검색

pinboard 검색 창에서 `#`을 누르면 태그 목록 검색 루틴으로 전환됩니다.
각 태그 별 갯수와 tag가 부여되지 않는 북마크 갯수가 표시됩니다.

이 화면에서도 글자를 입력하여 특정 태그 목록만 검색이 가능합니다.

![](https://farm4.staticflickr.com/3924/14472009270_a1b61866e9.jpg)

선택 항목에서 `enter`나 `tab`을 입력하면 해당 태그 목록에서만 검색할 수 있습니다.

![](https://farm3.staticflickr.com/2896/14658696065_84275c6143.jpg)

여러개의 태그 그룹에서 북마크를 검색하는 기능도 제공됩니다.
아래는 .adn와 programming 태그 그룹에서 bookmark를 검색하는 화면입니다.

![](https://farm4.staticflickr.com/3906/14472089318_d9a6afa9a3.jpg)

### 마지막에 참조했던 bookmark 목록 보기

`pblog`(ctl-shift-cmd-l) 명령을 수행하면 최근에 브라우저로 열었거나 복사한 북마크 목록이
표시됩니다. 이 화면에서도 검색 명령이 지원됩니다. 

각 북마크 별로 어떤 태그 그룹에 속해있는지, 몇 번 참조를 했는지 등의 정보가 표시됩니다.
아래 예에서 `Splunk Storm`이라는 bookmark는 두 차례 접근이 되었습니다. `alt`키를 누르면 이 화면에서
해당 항목을 초기화할 수 있습니다.  다른 창에서 `alt`키는 해당 북마크를 삭제하는 기능으로 동작하는데,
이 화면에서는 참조 정보만 초기화합니다.

최근에 접근된 bookmark가 윗쪽에 표시가 되기 때문에 최근에 접근한 bookmark를 빠르게 살펴보기 위한
용도로 활용하면 좋습니다. 

![](https://farm3.staticflickr.com/2905/14472050540_ee34438d1a.jpg)

### alfred-pinboard에서 검색했던 log 보기

`pbhis`(ctl-shift-cmd-h) 명령을 `pblog`와는 달리, 실제 goto나 copy를 하지 않더라도 최근에
alfred-pinboard를 이용해서 검색했던 정보를 보여줍니다. 검색에 사용했던 목록과 그 검색 항목의 결과가
몇 개 있는지 정보를 한 눈에 볼 수 있습니다.

자주 사용한 검색 목록을 상단에 유지하기 위해서는 `ctl`을 눌러서 `mark` 명령을 사용하면
됩니다. mark된 목록은 최근에 사용이 되지 않더라도 상단에 유지됩니다. 

![](https://farm3.staticflickr.com/2909/14655532701_4ab2865018.jpg)

### 자주 참조하는 bookmark 따로 모아 보기

`pbs`(ctl-shift-cmd-s) 명령은 mark로 지정한 bookmark 목록만 따로 모아서 보여줍니다.
mark된 북마크는 앞에 별표가 표시되어 다른 북마크와 구별됩니다.

북마크 목록에 mark 표시를 하기 위해서는 bookmark 위에서 `ctl`을 누르고 enter를 누르면 됩니다.
이미 mark된 bookmark에 해당 명령을 다시 수행하면 Unmark가 됩니다.

![](https://farm6.staticflickr.com/5496/14472152358_c2bd6f83c3.jpg)

### 북마크 출력 순서 바꾸기

검색 창에서 출력되는 순서를 바꾸기 위해서는 `!`나 `^`를 누르면 됩니다.

- `^l` : 가장 많이 접근되는 bookmark가 먼저 출력됩니다.
- `^d` : 기본 출력 순서는 가장 최근에 추가한 bookmark가 먼저 출력됩니다. `^d`는 가장 예전에 추가했던
  북마크가 먼저 출력됩니다.
- `^a` : 북마크의 타이틀 순으로 정렬해서 출력합니다.
- `^z` : 북마크의 타이틀 역순으로 정렬해서 출력합니다. 

![](https://farm4.staticflickr.com/3836/14655556771_dd98a944d6.jpg)

### 북마크 검색 명령어

- 기본 검색어
	- `pba query` 명령어는 타이틀, 설명, tag 목록에 [query]가 들어간 목록을 검색해서 출력합니다.
- and 검색어 
	- `pba q1 q1`은 타이틀, 설명, tag 목록에서 q1과 q2가 동시에 들어간 목록을 출력합니다. 이 때 q1, q2는
	꼭 같은 타이틀 목록에 나올 필요는 없습니다. q1이 타이틀에 q2가 설명란에 적혀 있어도 검색됩니다.
- or 검색어 
	- `q1`이나 `q2`가 들어간 모든 bookmark를 검색할 때는 `pba q1 | q2`와 같이 `|`를 이용하면 됩니다.
- not 검색어   
	- `q1`은 포함되었으나 `q2`가 포함되지 않는 북마크를 검색할 때에는 `-`를 사용합니다. (ex. `pba q1 -q2`)

### 메모 검색(full-text)

메모 검색은 full-text 검색이 가능합니다. 메모의 타이틀 뿐만 아니라, 실제 메모 내용도 검색됩니다.
full-text 검색을 하기 위해서는 `pbreload` 명령이 아닌
[pinboard-download.py](https://raw.githubusercontent.com/jmjeong/alfred-extension/master/alfred-pinboard/pinboard-download.py)를
이용하여 pinboard 내용을 download 받아야 합니다. 설치 단계에서 부가항목에 있는 cron tab에 사용되는
script가 이 script입니다.

Pinboard 사이트가 3초에 한번씩만 API 접근이 가능한데, 모든 메모의 내용을 local cache로 가져오기
위해서는 각 메모 당 API를 한번씩 호출을 해야 합니다. pbreload에서 이 내용을 다 가져오기에는 기다려야
하는 시간이 많아지기 때문에 `pbreload`에서는 타이틀만 가져오고, 실제 본문 내용은 별도의 script에서
처리하도록 되어 있습니다. 

### pocket으로 보내기

북마크에서 `shift` 키를 누르면 해당 북마크의 내용을 pocket으로 보내는 기능을 지원합니다. 

![](https://farm6.staticflickr.com/5495/14472699589_72328f223a.jpg)

pocket으로 보내는 기능을 사용하기 위해서는 `pbauthpocket` 명령을 사용해서 pocket에
인증을 한번 거쳐야 합니다.

![](https://farm3.staticflickr.com/2915/14679290133_47fc080f2b.jpg)
