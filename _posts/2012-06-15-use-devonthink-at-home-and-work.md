---
layout: post
title: Devonthink 두 곳에서 사용하기
description: 
category: 
tags: mac
---

Devonthink 데이타를 dropbox에 넣어두고 회사와 집에서 사용을 하고 있다. 데이타의 integrity를 보장하기
위해서 데이타를 두 곳에서 동시에 수정을 하면 안 된다. 이를 위해서 Folder action을 이용해서 dropbox에
특정 파일이 존재하면 자동으로 Devonthink를 중단하는 apple script를 작성해서 사용을 해 보았으나, 한쪽
computer가 sleep 상태에 들어가면 script가 수행되지 않는 문제가 있다.

이를 해결하기 위해 screensaver가 동작을 하면 자동으로 devonthink를 중단시키고, 비활성화되면 다시
load하는 방법을 테스트 해 봤더니 잘 동작을 한다.

1. [ScriptSaver : screensaver-triggered AppleScript](http://swannman.github.com/scriptsaver/)를 인스톨한다.

2. Activation script로 quitdevonthink 를 지정한다. quitdevonthink는 다음과 같이 구성되어 있다.

	tell application “DEVONthink Pro” to quit

3. Deactivation script로 rundevonthink 를 지정한다. 다음과 같은 내용이다.

	tell application “DEVONthink Pro” to exists
	
4. Screen saver에서 ScriptSaver가 동작하도록 한다.
