---
layout: post
title: Outwitters
modified: 
category: ios 
tags: ios
image:
  teaser: t-outwitters.jpg
---

# Outwitters 게임 

iOS용 완성도 높은 턴제 전략 게임. AppStore's Best of 2012에 뽑혔고, 여러 수상 이력이 있다.
iPhone, iPad를 동시에 지원한다. 
  
- [프로그램 URL](https://itunes.apple.com/app/outwitters/id432969074?mt=8)
- [OSN Replays](http://osn.codepenguin.com/replays)


## 장점

- Asynchronous 게임을 지원해서 시간 날 때 한 턴씩 진행이 가능하다. 4일 이내만 진행되면 게임이 지속된다.
- 룰은 간단한데 마스터하기가 쉽지 않다. 리그 별로 사람들과 경기를 해서 다양한 전략을 맛볼 수 않다.
- 인 앱이 있기는 한데 광고 제거와 종족 추가 정도이고, 현질의 위험이 적다. 
- [Outwitters sports network](http://osn.codepenguin.com/replays)라는 fan이 만든 비공식 replay
  사이트가 있어 고수의 경기를 구경할 수 있다.
- 앱 내에서 한글 채팅 지원한다.
- Game Center 연동이 원활해서 친구들과 게임이 쉽다. 2:2 대전도 지원한다
- 전체 턴을 한꺼번에 보내는 방식이라 한 턴 기다리는 동안 다른 경기 진행이 가능하다.
- 안개 기능 지원으로 정찰, 급습, 물량전 등 다양한 전술이 가능하다.
- 매 시즌마다 리그전을 지원한다.

## 단점

- 업데이트가 나오기는 하지만 active하게 개발되고 있지는 않다. 
- 사람에 따라 Push notification이 안오는 경우가 있다.

## Replays

<iframe width="420" height="315" src="//www.youtube.com/embed/Cvy6Q_5Qldw" frameborder="0" allowfullscreen></iframe>

# Drafts Action

- [Script Link](http://drafts4-actions.agiletortoise.com/k/1LA)
  - ADN에 replay link를 포스팅하기 위한 [Drafts 4](https://itunes.apple.com/app/id905337691?mt=8)
    action script

## Drafts action script

```js
content = getClipboard()

try {
    var id = /id=(.*)/i.exec(content)[1]
} catch(e) {
    alert('Invalid clipboard url');
    stopAction();
}

osnLink = '[OSN](http://osn.codepenguin.com/replays/view/'+id+")"
outwitterLink = "[OutWitters](http://s.jmjeong.com/f.php?id="+id+")"

link = '\n\n- '+osnLink+'\n- '+outwitterLink;
setText(link)
```

Outwitters Link를 ADN에서 유효한 link로 인식하지 않아, OutWitters link는
서버에서 `outwitters://` link를 반환하도록 하였다.

## 사용법
1. Outwitters 프로그램에서 long-click으로 link 복사
2. Drafts 4 앱을 수행하여 OW 버튼 클릭
3. Post to ADN action을 이용하여 riposte로 posting

![](/images/outwitters.jpg)
