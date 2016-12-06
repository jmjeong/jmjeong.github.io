---
title: GemsOfWar Bot 개발
description: node.js를 이용하여 GemsOfWar bot 개발
layout: single
tags: node
category: node
---

Link : [https://telegram.me/gemsofwar_bot](https://telegram.me/gemsofwar_bot)

## 개발

- node.js로 제작
- 사용 npm
  - node-telegram-bot-api : telegram bot 
  - async : flow control
  - lodash : utility 
  - cron : 매일 2시, 16시에 웹 사이트에서 변경된 데이타를 읽어옴 
  - marked : `file`명령을 위해 md 파일을 HTML로 변경 
  - moment : 날짜/시간 처리 함수 
  - node-scrapy : 웹 사이트 데이타 crawling
  - node-static : http://gow.jmjeong.com 으로 file 정보 제공 
  - request : traits 정보를 읽어옴 
  - require-reload : 웹 사이트 데이타가 업데이트 되고 난 후 다시 메모리 적재하는 용도로 사용 
  - redis, redis-delete-wildcard : redis client 
- data - 웹에서 scrape해 온 데이타로 자동으로 구성 
  - data.json : troop, weapon, class information
  - data-kingdom.json : kingdom data
  - data-troop-traits.json : troop, class의 traits 정보 
  - data-traits.json : `st` 명령 처리를 위해 traits 정보만 따로 추출
  - data-traits-info.json : `stu color` 명령 처리를 위해 kingdom 데이타로부터 추출 
- 명령어
  - search : 데이타 검색. s, si, sd, st, stt, stu 
  - admin : 웹에서 데이타 fetch 및 last history 참고
  - help : 도움말
  - file : traitstone, troop list 파일 전송용
  - noti : redeem code 전달
- command help
	- `/s troop [index]` - search troops or weapons
	- `/si troop [index]` - search troop image
	- `/sd desc [index]` - search spell description
	- `/st traits` - display traits info
	- `/stt traits` - search troops with traits
	- `/stu TraitStone` - search troops and traits using TraitStone
	- `/stu TraitStoneColor` - ex) stu brbl (brown blue)
	- `/stu *` - display All arcane TraitStone
	- `/file t|k` - t: TraitStone, k: kingdom troop

### Redis Data Structure

- `gow:RELOAD_DATA` - admin reload, cron 등에서 데이타가 변경 시, 데이타 loading 을 위한 FLAG

- `gow:history:index` - history 기록을 위한 next index 값
- `gow:history:data` - list. 접속 로그
- `gow:history:data:[idx]` - hash. 접속 로그. `{time: , msg: }`

- `gow:user:[userid]` - `{first_name: , last_name: , username: }` telegram bot log 정보 

- `gow:notification:list` - list. 알림 받을 목록 
- `gow:notification:history:index` - notification 기록을 위한 next index 값
- `gow:notificatoin:history:data` - list. notification 로그 
- `gow:notification:history:[idx]` - hash, notification 로그, `{time: , msg: }`
  
## 데이타 가공

- http://ashtender.com/gems/troopquery 데이타 활용
- Chrome postman, Chrome Developer tool을 이용하여 network traffic 조사
  - chrome image downloader extension을 이용하여 image download(이미지 사용하지 않음)
  - 기본 정보는 HTML으로 출력
  - traits 정보는 Ajax를 이용하여 API 호출하고 결과값은 JSON으로 반환
  
- node-scrapy를 이용하여 HTML을 json으로 변환하는 루틴 제작 
  - chrome developer tool의 copy selector를 이용하여 모델 작성
  - traits 정보는 json 으로 제공해 줌 - async.parallel을 이용하여 정보 읽어 옴

## 목표

- [GemsOfWar](http://gemsofwar.com) Puzzle-RPG hybrid from the creators of Puzzle Quest
- 매 주 새로운 카드 추가, 카드에 skill, traits, kingdom, type 등 다양한 정보가 있음
- 웹 사이트 속도가 느리고, 데이타의 검색이 지원되지 않음
- 길드가 활성화되어 통신 수단으로 telegram 사용
- telegram bot api 테스트 겸 @GemsOfWar_bot 제작
- 새로운 데이타가 추가되더라도 유연하게 처리
