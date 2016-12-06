---
layout: post
title: "alfred-pinboard tip"
description: "alfred pinboard를 bookmark처럼 활용하는 법"
tags: alfred pinboard python
image:
 teaser: t-alfred-pinboard-1.png
---

Github에 공개한 [alfred-pinboard](https://github.com/jmjeong/alfred-extension/tree/master/pinboard)를
이용한 bookmark 관리 Tip입니다.  저는 pinboard로 모든 자료를 옮긴 후에 safari에는 pinboard에
bookmark를 저장하는 bookmarklet과 pinboard로 가는 link만 버튼으로 남겨두었습니다.

<!-- more -->

## Updated [2014-05-28 Wed]

[alfred-pinboard v2]({% post_url 2014-05-26-alfred-pinboard-v2 %}) 에서 mark 기능을 이용하여 더 편하게 관리할 수 있습니다. 

![](/images/pinboard-history.jpg)

`pbtag`로 해당 tag를 한번 수행 후, `pbhis` 명령을 이용하면 마지막에 수행했던 검색 명령을 볼 수
있습니다. 여기서 `Cntl`-`Enter`를 이용하여 고정시켜 놓으면 항상 `pbhis`를 입력해 특정 bookmark를
손쉽게 볼 수 있습니다.

---


<!-- more -->

hotkey로 특정 tag에 속한 bookmark 목록을 띄워주는 방법입니다.

## 동작

mac에서 ctl-shift-command-n 을 누르면  nemus에 속한 다음 alfred 창이 뜹니다. 여기서 title 검색과 enter 키를 눌러서 직접 이동이 가능합니다. 

![](http://farm4.staticflickr.com/3721/12638537425_903aa4e926.jpg)

pinboard에 nemus tag에 아래 3개의 bookmark를 등록해 두었습니다. 

![](http://farm6.staticflickr.com/5479/12639022764_afa927a736.jpg)

## 설정 방법

### alfred에 script filter 등록 

alfred에 설치된 pinboard workflow에서 우측 상단의 + 를 누르고, Input->Script Filter를 눌러서 다음과 같이 설정합니다. 

![](http://farm4.staticflickr.com/3793/12639065234_047130ce9b.jpg)

Hot Key 뿐만 아니라 nn 이라는 키워드로도 열 수 있도록 했습니다.  Script 항목에 다음과 같이 사용합니다. 

	python main.py tags "nemus→{query}"

→ 앞에 쓴 nemus가 tag 명입니다. 

### alfred에 hot key 등록 

Triggers->HotKey를 추가한 후, HotKey를 등록합니다. 

![](http://farm6.staticflickr.com/5504/12639305094_72f297c50a.jpg)

### template 연결 

그 후 추가된 각 Template을 다음과 같이 연결해 줍니다. 

![](http://farm4.staticflickr.com/3783/12638812813_3dc4cf8bf2.jpg)

Bookmark 목록을 변경하고 싶은 경우에는 pinboard 사이트에서 수정하면 됩니다. 
