---
layout: post
title: MacOS Emacs 한글 입력
description: 
category: emacs
tags: emacs mac
---

Mac Lion에서 Emacs는 AquaEmacs, Cocoa Emacs등 다양하게 있는데, 이것 저것 써 봐도 Vanila Emacs가 제일 쓰기 편한 것 같다. 예전에는 source를 받아다가 compile해서 사용을 했는데, 이제는 binary package를 배포해 주는 site가 생겼다.

Lion Mac에서 [Baram 입력기][1]로 교체해서 사용한다. 라이온에서 1.5.2가 가장 안정적으로 동작한다.

사용자 정의 한영 전환 단축키를 익숙한 [Shift-Space]로 변경하고, Emacs를 수행할 때는 영어 모드로, 리맵퍼는 사용안함으로 설정한다.

‘각 도큐멘트에 대해 다른 입력 소스 허용’ 이 설정이 켜 있지 않으면, Emacs에서 영문 모드로 사용하다가 다른 프로그램(ex. iterm)에서 한글을 입력하다가 Emacs로 돌아오면 한글모드 입력이 되는 문제가 있다.

Emacs의 한영전환은 아래 설정으로 [Shift-Space]로 변환한다. 2벌식 사용자는 (setq default-korean-keyboard “3″)라인을 주석처리하면 2벌식으로 동작한다.

```elisp
;; Korean Setting
(set-language-environment "Korean")
(setq default-korean-keyboard "3")
(setq input-method-verbose-flag nil input-method-highlight-flag nil)
(prefer-coding-system 'utf-8) ; utf-8 환경 설정
```

Baram 1.5.2와 Emacs 24가 호환이 맞지 않는지 영문 Only 모드로 설정이 되지 않는다. [Shift-Space]를 누르면 Baram에서 먼저 한글모드로 변환이 되어서, 기존의 Default 설정인 Control- 키를 눌러서 한-영 전환을 해야 한다. 해결책을 찾을 때까지 당분간 Emacs23을 사용해야 할 것 같다. [구름입력기][5]에서 영문 Only 모드로 설정될 수 있는지도 한번 확인해야 할 듯

   [1]: http://baramim.blogspot.kr/
   [2]: http://jmjeong.com/wp-content/uploads/2012/06/baram-1.5.2.png (baram-1.5.2.png)
   [3]: http://jmjeong.com/wp-content/uploads/2012/06/baram-application.png (baram-application.png)
   [4]: http://jmjeong.com/wp-content/uploads/2012/06/lang-text.png (lang-text.png)
   [5]: http://gureum.org/
  
