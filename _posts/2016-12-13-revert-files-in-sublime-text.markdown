---
layout: post
title: SublimeText 에디터에서 여러 개의 파일 되돌리기
description:
category:
tags: sublimetext
---


sublime text에서 find & replace로 다 수의 파일을 업데이트 한 후, 파일을 저장하고 싶지 않는 경우...  
창을 닫은 경우, 파일을 저장할 것인지 물어보는 창이 뜨고, `Don``t Save` 버튼을 누르는 것이 불가능할 때...  
앱을 kill 했다가 다시 띄운 경우에도 열었던 파일을 다시 열어서 띄워주는 경우...    

`Ctrl-``을 눌러서 명령어 창을 연 다음 python 명령을 내리면 됩니다.

```
[v.run_command("revert") for v in window.views()]
```