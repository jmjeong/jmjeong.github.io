---
layout: post
title: twittering-mode.el patch
description: 
category: emacs
tags: emacs
---

[Twittering mode](http://www.emacswiki.org/emacs/TwitteringMode)는 emacs을 위한 twitter
client이다. git에 올라와 있는 0.8 버젼을 사용하고 있는데, 두가지 불편한 점이 있어서
[patch](http://github.com/jmjeong/twittering-mode)했다. 최신 trunk에 반영되었다.

#### 문제점

- 140글자를 넘어가는 경우 posting이 안 된다. 다른 client 처럼 몇 자가 넘었는지 표시를 해 줬으면 한다.
- bit.ly, tiny.url 처럼 URL 단축화 기능을 지원했으면 한다.

#### 해결

1. twittering-update-status-from-minibuffer 함수에서 posting 하기전에 string 길이가 140보다 크면 다시 입력을 받게 했다.

2. minibuffer keymap에 Key를 추가하여 <F4>를 누르면 URL을 줄여서 치환하게 했다. 웹을 검색해 보니 URL
축약 기능을 하는 smallurl.el 파일이 공개되어 있어서 그 곳에 있는 함수를 이용했다.

```elisp
(defun twittering-update-status-from-minibuffer (&optional init-str
                                                           reply-to-id)
  (if (null init-str) (setq init-str ""))
  (let ((status init-str) (not-posted-p t) (map minibuffer-local-map))
    (while not-posted-p
      (define-key map (kbd "<f4>") 'smallurl-replace-at-point)
      (setq status (read-from-minibuffer "status: " status map nil nil nil t))
      (while (< 141 (length status))
        (setq status (read-from-minibuffer (format "(%d): "
                                                   (- 140 (length status)))
                                           status map nil nil nil t)))
      (setq not-posted-p
            (not (twittering-update-status-if-not-blank status reply-to-id)))
      )
    ))
```
