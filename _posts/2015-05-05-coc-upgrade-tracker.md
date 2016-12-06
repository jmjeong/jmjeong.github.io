---
layout: post
title: clash of clans upgrade tracker
modified: 
category: node
tags: node
image:
  teaser: t-coc-tracker.jpg
---

[http://coc.jmjeong.com](http://coc.jmjeong.com)

Clash of Clans 타운 홀 별 업그레이드 정보를 보여주고 기록하는 웹 사이트이다.
[MEAN stack](http://mean.io)으로 개발하였다. 

## Upgrade 상태 정보

![overview](/images/coc/coc-overview.jpg)

- 얼마나 걸리는 Upgrade인지, 남은 시간, 종료 시간 표시
- 일반, Research, Hero는 색으로 구분하여 표시

## 통계 정보

![summary](/images/coc/coc-summary.jpg)

- 설정된 town hall을 최대로 올릴 때까지 드는 리소스와 시간
	- builder 갯수를 감안하여 시간 계산
		- 위의 예는 9홀 풀 업까지 5장인으로 174일이 걸리고, 연구는 221일 걸린다.
	- 리소스는 building과 research, 그리고 wall을 구분하여 표시
		- 9홀 풀업까지 건물 업그레이드에 224.9M 골드, 47.6M 엘릭서, 4.1M 다크 엘릭서가 필요하다. Research에는 39.8M 엘릭서, 645k 다크엘릭서가 필요하다.
		- 벽의 경우에는 Lev 8이후에는 elixir로도 업그레이드 가능하다.
- 업그레이드 상태를 바탕으로 현재까지의 투자한 리소스와 시간을 표시한다.

## 각 카테고리 별 업그레이드 정보

![category-upgrade](/images/coc/coc-category-upgrade.jpg)
![category-upgrade-summary](/images/coc/coc-category-upgrade-summary.jpg)

- 다음 업그레이드에 들어가는 리소스 및 걸리는 시간
	- 예) 남아 있는 archer tower 수와 각 업그레이드에 들어가는 리소스와 시간을 표시한다. 
- 카테고리 별로 최대로 올릴 때까지 드는 리소스와 시간, 현재까지 들어간 리소스와 시간 표시
- Resource 탭에는 하루 생산되는 골드, 엘릭서, 다크엘릭서 총량 표시
- Research와 Hero 탭에는 업그레이드 시 증가하는 dps와 hp를 툴팁으로 표시

## [Upgrade] 탭

![upgrade](/images/coc/coc-upgrade.jpg)

- 다음 업그레이드 할 수 있는 모든 목록 표시
- 시간, 골드, 엘릭서, 다크 엘릭서로 정렬 가능
- 업그레이드를 즉시 완료할 때 드는 Gem 갯수 표시
- 진행 중인 업그레이드는 완료 시간과 이후 올릴 업그레이드 표시

## [Log] 탭 - 계정 등록 후 이용 가능

![share](/images/coc/coc-log.jpg)

- 업그레이드 완료 내역 
- 이름으로 검색 예) Queen

## 공유 기능 - 계정 등록 후 이용 가능

![share](/images/coc/coc-share.jpg)

- 현재 Upgrade 상태를 친구에게 [읽기 모드]로 공유 기능 제공
