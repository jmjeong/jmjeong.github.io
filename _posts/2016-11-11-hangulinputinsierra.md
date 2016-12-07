---
layout: post
title: macOS Sierra에서 한글 입력
description: 
category: mac
tags: mac
---

alfred 3 에서 keyboard layout을 US 로 설정을 해 두는데도,  첫글자가 한글로 나오는 문제가 있습니다[^1]. 
Java app에서 space를 누르는데도 공백이 추가되지 않는 문제도 있고요. 
 
Elcapitan에서는 문제가 없었는데, Sierra 올라오면서 문제가 생겨서 OS와 뭔가 안 맞다고 생각을 했는데,
Baram 입력기와 뭔가가 맞지 않아서 생기는 문제네요.  내장 입력기로 바꾸었더니 문제가 사라졌습니다.
 
내장 입력기 대신 바람입력기를 사용하게 되었던 것이, 
shift-space 입력 단축키와와 한글 상태에서는 단축키가 안 되는 이슈 때문이었습니다.
한글 상태에서 단축키가 안 되는 이슈는 일부 완화되었고, 
shift-space는 [입력 메뉴에서 다음 소스 선택]을 안 쓰는 키(ctrl-shift-f12)로 할당하고, 
그 키를 다시 매핑하는 방법으로 사용해 보기로 했습니다. 
 
한글 입력기 상태에서는 Ctrl-A, E, F, B, N, P도 동작하지 않는 문제가 있어, 
keyboard maestro를 이용하여 [키를 재 설정](http://d.jmjeong.com/MwBk+)하여 사용하고 있습니다.

Alfred에서 Ctrl-P, Ctrl-N이 action으로 동작하는 불편함이 있어, action key를 `tab`으로 변경해서 
쓰다가 설정 변경[^2] 후에 원래 대로 `ctrl`로 변경하여 사용합니다. 

[^1]: alfred option - apperance - focusing을 compatibility mode로 변경하면 해결된다고 합니다. 
[^2]: alfred option - apperance - focusing to "Compatibility mode"