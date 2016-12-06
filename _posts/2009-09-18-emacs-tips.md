---
layout: post
title: Emacs Tip
description: 
category: emacs
tags: emacs
---

## 현재 buffer에 file path를 추가

내장 함수로 있을 것 같은데, 찾아봐도 없다.

```elisp
  ;; insert-path macro
  (defun insert-path (file)
    "Insert a path into the buffer with completion"
    (interactive "GPath: ")
    (insert (expand-file-name file)))
  
  (global-set-key (kbd "C-x C-i") 'insert-path)
```

## C-s C-w 커서 아래에 있는 단어 검색

## info 파일을 local browse하기

`C-h i`에 prefix를 붙이면 파일 지정이 가능하다 

    C-u C-h i common/cedet.info

## Emacs화면을 full screen화면으로 보기

[- EmacsWiki FullScreen](http://www.emacswiki.org/emacs/FullScreen).

Windows, X, MacOS에 따라 동작방식이 다르다. maxframe.el을 이용해서 Meta-RET로 toggle 방식으로 처리가
되도록 변경해서 사용했다

```elisp
;; maxframe.el [2009-10-22]
(require 'maxframe)
;(add-hook 'window-setup-hook 'maximize-frame t)

(defvar my-fullscreen-p t "Check if fullscreen is on or off")

(defun my-toggle-fullscreen ()
  (interactive)
  (setq my-fullscreen-p (not my-fullscreen-p))
  (if my-fullscreen-p
      (restore-frame)
    (maximize-frame)))

(global-set-key (kbd "M-RET") 'my-toggle-fullscreen)
```

## Emacs Recent file list 관리

```elisp
;; recentf stuff
(require 'recentf)
(recentf-mode 1)
(setq recentf-max-menu-items 25)
(global-set-key "\C-x\ \C-r" 'recentf-open-files)
```

`\C-x \C-r`은 `find-file-read-only`이 default keymapping으로 정의되어 있다. 이를 최근 열린 파일을
여는 명령어로 대치하여 사용하자.

## Emacs lisp expression의 수행 결과를 buffer에 insert할 때

  -   **M-::** eval-expression
  -   **C-X C-e:** eval-last-sexp
  -   **C-M-x:** eval-buffer

명령어에 C-u prefix를 붙이면 수행결과가 현재 current buffer에 insert된다.
문서내에 현재 수행 중인 emacs의 버젼 명을 기록하고 싶을 때 C-u M-x version 하면 된다.

## dired mode에서 directory의 파일을 최근 편집된 순으로 보기

Dired-x 모듈을 dired 모드 쓸 때 로딩하고, 원하는 directory에 .dired 파일을 만들어서 local
variable들을 설정하여 사용한다. 홈페이지의 블로깅 article들을 최근 변경한 순서로 보기 위한 용도로
세팅하여 사용 중이다.

```elisp
(add-hook 'dired-load-hook
          (lambda ()
          (load "dired-x")
))
```

.dired 파일 내용 

    Local Variables:
    dired-actual-switches: "-lat"
    dired-omit-mode: t
    End:

## 현재 창에 보이는 font 크기 조절하기(Emacs 23)

Presentation 중에서 현재 보이는 창의 글자 크기를 조절할때 유용
-   C-X C-= : Increase the default face height by one step (text-scale-adjust inc)
-   C-X C&#x2013; : Decrease the default face height by one step
-   C-x 0   : Reset the default face height to the original default

-   <http://groups.google.co.kr/group/gnu.emacs.help/browse_thread/thread/8c8145102dadc34c>
-   <http://stackoverflow.com/questions/534307/set-emacs-defaut-font-face-per-buffer-mode>

- Dired에서 path 이름 복사

  -   w : dired-copy-filename-as-kill
  -   C-u 0 w : path 이름까지 복사

## EmacsW32에서 bell 소리 없애기

X 상에서야 xset b off 하면 나오는 삐삐 거리는 벨 소리를 없앨 수가 있지만, Win32상의 emacs에서는
없애는 법이 없나 찾아보았다.  가장 손쉽게 할 수 있는 방법이 (setq visible-bell t) 로 하는 방법인데
화면 frame이 번쩍번쩍 거려서 보기가 싫다.

이런 용도로는 set-message-beep를 사용한다.

```elisp
(set-message-beep 'silent)
```

## 모드별로 font 설정 바꾸기

Org 모드에서는 fixed with font인 NanumGodicCoding을 사용하는데, mail에는 가변폭 폰트를 사용하고 싶다. 
`variable-picth-mode` 값을 세팅하면 된다(Emacs 23에서만 가능). 

```elisp
(setq message-mode-hook
     (quote (
     (lambda () (variable-pitch-mode nil)) 
     )))
```     

