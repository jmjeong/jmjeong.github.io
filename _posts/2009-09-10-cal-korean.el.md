---
layout: post
title: cal-korean.el
description: 
category: emacs
tags:  emacs
---

Emacs의 calendar에 대한민국 음력을 표시해 주는 elisp 파일이다. 

대한민국에서 사용하는 음력은 Emacs에서 기본 제공하는 cal-china.el과 많은 날짜들이 일치하지만,
Timezone 때문에 1시간의 차이가 난다. cal-china.el 파일을 기반으로 대한민국 음력을 지원하는 모듈을
만들었다.

- [파일 download link](http://github.com/jmjeong/my-dot-emacs/blob/130e8d593cc49ca5e5d62d5b4fdb4c79c24aea90/cal-korean.el)

기본적인 사용은 .emacs 파일에 아래와 같은 내용을 추가한다. 

```lisp
;; calendar korean lunar
(if (= emacs-major-version 23)
	(require 'cal-korean)
  (require 'cal-korea22))

;; 음력 표시할 때 길게 표시
(eval-after-load "cal-korean"
  '(progn
	 (setq calendar-korean-print-long-description t)
	 ))
```

M-x calendar를 구동하여 'p l'을 누르면 오늘 날짜에 해당하는 음력이 출력된다


또한 'g l'을 누르면 특정 날짜의 음력날짜를 입력받아서, 그 날에 해당하는 양력 날짜를 출력한다. 

```lisp
(setq calendar-korean-print-long-description nil)
```

long-description 값이 nil일 때는 간단한 포맷으로 출력한다 

diary mode나 org-mode를 위한 함수또한 추가되었다. Org-mode의 agenda를 표시할 때 diary항목도 추가하기 원할 때는 아래 변수를 세팅하면 된다. 

```lisp
;; diary file 지정
(setq diary-file "~/diary")
;; diary entry 포함
(setq org-agenda-include-diary t)
```

**Diary File Format**

```
    %%(diary-anniversary 5 1) 노동절
    %%(diary-lunar-anniversary 1 1) 설 - %s
    %%(diary-lunar-anniversary 8 15) 추석 - %s
    %%(diary-lunar-anniversary 4 8) 석가탄신일 - %s
    
    ...
    
    %%(diary-lunar-anniversary 12 4 1970) 정재목 - %s(%d)
```

일반적으로 diary 파일에서 사용하는 것처럼 음력에 해당하는 날짜를 calendar에 표시를 해 준다. 
앞의 그림에서 `darkred` 로 표시된 것이 기념일에 해당하는 날짜이다. '추석'또한 기념일로
세팅이 되어 있어서 해당 날짜가 `darkred` 로 표시가 되었다. 

cal-korean.el 에서 새로 추가 지원되는 함수는 다음과 같다. 

-   `(diary-korean-date)`
    
    각 날짜에 속하는 음력 날짜를 출력한다. 주로 org-mode agenda에서 양력 날짜와 함께 음력을 출력할 때
    사용한다.

-   `(diary-lunar-date MONTH DAY YEAR &optional LEAP MARK)` 
    
    diary-date에 상대되는 음력 함수이다. MONTH, DAY, YEAR 각 항목을 t로 지정하여 무시할 수 있다. 
    사용방법으로 '%% (diary-lunar-date 1 1 t) 설날 - %s'와 같이 사용되고 이 중 '%s'는 출력되는 format에 맞는
    음력 날짜로 치환된다.

-   `(diary-lunar-anniversary MONTH DAY &optional YEAR LEAP MARK)` 
    
    diary-anniversary에 상대되는 음력함수 이다. YEAR가 입력된 경우에는 해당 기념일이 기념일로부터 
    몇 년이 지났는지를 계산하여 출력한다. 
    
    사용 방법으로는 '%%(diary-lunar-anniversary 12 4 1970) 정재목 - %s(%d)' 와 같이 되고 %s는 음력 날짜로, %d는 해당하는 음력날짜로부터 몇년이 지났는지에 대한 값이 치환됩니다.  윤달인 경우에는    LEAP에 t를 입력하면 된다.  %s %d가 이 순서대로 나와야 한다.
	
    출력결과는 '정재목 - 음력 12월 4일(37)'이 된다.


