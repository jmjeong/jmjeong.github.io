---
layout: post
title: Emacs용 Mail client 사용기
description: 
category: emacs
tags: emacs
---

### Gnus

KLDP에서 Gnus의 최신버전이 예전버전과는 달리 한글 입출력이 깔끔하게 [잘 지원된다](http://kldp.org/node/103560)는 글을 보고, Thunderbird와 함께 두 달 정도 사용을 했다. Emacs 23의 snapshot에 Gnus v5.13이 들어가 있고, mac에서는 별도의 utility 설정 없이도 gmail이나 회사 IMAP 메일로 접근하여 메일을 읽고 쓰는 것이 큰 문제가 없이 동작을 한다.

![](http://farm4.staticflickr.com/3709/13172493964_444951b6d9_o.png)

```lisp
(setq user-mail-address "jmjeong@nemustech.com")
(setq user-full-name "Jaemok Jeong")

(setq gnus-select-method '(nnimap "nemustech"
    (nnimap-address "mail.nemustech.com")
    (nnimap-server-port 993)
    ; 로그인 정보 파일을 사용하여 자동 로그인 하고자 할 경우 사용
    (nnimap-authinfo-file "~/.imap-authinfo")   
    (nnimap-stream ssl)))
;; .imap-authinfo file format 
;;  
;;  machine mail.nemustech.com login MyEmailAddress password MyPassWord port 993
;;

(setq gnus-show-threads t)
(setq gnus-thread-indent-level 2)

(require 'bbdb)                                                       
(bbdb-initialize)                                                     

;(add-hook 'message-send-hook 'ispell-message)
(add-hook 'gnus-startup-hook 'bbdb-insinuate-gnus)

(setq bbdb-north-american-phone-numbers-p nil)
(setq bbdb-check-zip-codes-p nil)

(setq message-mode-hook
      (quote (
      (lambda nil (setq fill-column 72))
      turn-on-auto-fill
      bbdb-define-all-aliases
      )))
```

`gnus-select-method`를 이용하여 nnimap으로 설정하고, 매번 passwd를 물어보는 문제는 `.nnimap-authinfo` 파일에 인증 설정을 하여 해결하였다. [GnusEncryptedAuthInfo](http://www.emacswiki.org/emacs/GnusEncryptedAuthInfo)에 인증 암호를 encrypt하는 방법도 설명이 되어 있다.

10년 사이에 “Gnus package도 많이 발전했구나, 여러 open source에서 UTF-8지원이 공식화되다보니 따로
localization에 대해서 고민을 안해도 되는구나” 생각을 하다가 [Gnus의 느린속도](http://www.emacswiki.org/emacs/GnusSpeed)에 불만을 갖게 되었다. [Rmail](http://www.gnu.org/software/emacs/manual/html_node/emacs/Rmail.html), [Mew](http://www.mew.org/en/), [WanderLust](http://www.emacswiki.org/emacs/WanderLust), [VM](http://www.emacswiki.org/emacs/CategoryViewMail)등을 고민하다가 내가 왜 예전에 Gnus를 쓰다가
중단했는지를 알게되었다.

- 사용하면서 느끼는 Gnus의 단점 두가지 [2009-10-27 Tue]
	- **느린 속도** IMAP으로 online상의 여러 folder에 있는 메일을 읽어올 때나, 큰 첨부파일을 갖는 메일을 읽을 때는 답답하다. 속도 이슈로 매력적인 score 기능을 활성화시킬 수가 없다. Gnus가 thread화 되지 않으면 당분간 해결이 쉽지 않을 것 같다. Offlineimap을 이용하여 local로 imap folder를 sync하여 Gnus를 활용하면 어떨까? Mew에서는 mime parsing을 별도의 C utility로 만들어서 하던데 이런 방법도 concurrent emacs가 아니고도 해결할 수 있는 좋은 방안일 듯 하다.
	- **너무 많은 명령어** Gnus가 news reader로 제작되다보니, mail client로만 쓰기에는 기능이 너무 많다

### Rmail

Rmail은 Emacs의 기본적으로 내장되어 있는 mail viewer이다.

빠른 속도 IMAP 데이타를 `fetchmail`, `procmail`을 이용하여 local로 옮기고, RMAIL로 읽으니 mail, mutt 속도로 읽을 수 있었다. MIME Encoding 문제 Charset과 MIME decoding을 제대로 못하는 문제가 있다. 

- 참고 : [RmailMime](http://www.emacswiki.org/emacs/RmailMime)

![](http://farm3.staticflickr.com/2772/13172578364_9d6dc3a549_o.png)

### ViewMail

VM은 XEmacs에 내장되어 배포되고 있는 메일 client이다. 현재 VM version 8.0.12 버전까지 나와 있고,
Emacs에서도 문제없이 수행이 된다. Default 설정으로는 한글 encoding과 MIME decoding이 원할하지 않다. 이것저것 설정을 조정해가면서 쓸만큼 매력적이지 않아서 일단 패스.

![](http://farm8.staticflickr.com/7159/13172426543_4359ccf4e3_o.png)

### Wanderlust

[Wanderlust Homepage](http://www.gohome.org/wl/),
[email with wanderlust](http://emacs-fu.blogspot.com/2009/06/e-mail-with-wanderlust.html)에서 wanderlust에 대한 좋은 평들이 있다. 홈페이지는 몇년동안 수정이 되고 있지 않고, CVS에도 commit log가 꽤 오래전이다. Wiki에 update되어 있는 글들도 2006년 이후로는 올라와 있지 않다. Emacs 23에서 UTF-8을 잘못 encoding한다는 [보고](http://www.emacswiki.org/emacs/WlEmacsTwentyThree)도 있다. 좋은 장점에도 불구하고 오래되고, 설정하기 복잡하고, SEMI, APEL, FLIM등 외부 package에 의존성이 있다는 문제점이 있다.

![](http://farm4.staticflickr.com/3680/13172627694_4846aa891d_o.png)

Gnus보다 빠른 속도와 사용하기 편한 인터페이스, Offline IMAP supoort등의 장점이 많이 있었다. 하지만, SEMI(Emacs mime interface)가 상대적으로 예전 버젼이다보니 최신 gnus에 들어있는 것처럼 MS의 비표준 encoding에 대한 예외처리가 되어 있지 않다. `ks_c_5601-1987`을 `euc-kr`로 치환하는 것을 찾아보려 했으나, 문서도 많지 않고 해서 사용하지 않기로 했다. Gnus와 wanderlust를 동시에 사용하니, MIME쪽의 의존성 문제인지 Gnus쪽의 메일 처리가 이상해지는 문제도 있었다.

### Mew

![](http://farm4.staticflickr.com/3696/13172485103_c37ca2abc1_o.png)

일본에서 제작되어 다국어에 대한 고려가 많이 되어 있다. Gmail을 pop이나 IMAP을 통해 접근하여 메일을 읽는것이 가능하다. 체감속도는 wanderlust에 비해 약간 느리다.

```lisp
(setq mew-pop-size 0)
(setq mew-use-cached-passwd t)
(setq mew-passwd-timer-unit 999)
(setq mew-passwd-lifetime 999)
(set-default 'mew-decode-quoted 't)  
(setq mew-prog-pgp "gpg")
(setq mew-pop-delete nil)
(setq mew-config-alist 
;;Gmail
 '(
  ("default"
 ("name"      . "Jaemok Jeong")
 ("user"      . "jmjeong")
 ("mail-domain"   . "gmail.com")
 ("proto" . "+")
 ("pop-ssl"   . t)
 ("pop-ssl-port"  . "995")
 ("prog-ssl"  . "/opt/local/bin/stunnel")
 ("pop-auth"  . pass)
 ("pop-user"  . "jmjeong")
 ("pop-server"    . "pop.gmail.com")
 ("smtp-ssl"  . t)
 ("smtp-ssl-port". "465")
 ("smtp-auth-list" . ("PLAIN" "LOGIN" "CRAM-MD5"))
 ("smtp-user" . "jmjeong")
 ("smtp-server"   . "smtp.gmail.com")
 )
 ))
(setq mew-summary-form '(type (5 date) " " (14 from) " " t (70 subj) ))
```

### 총평(속도)

- OfflineImap 프로그램을 이용하여 9G가 넘는 IMAP folder를 Local machine으로 옮겨서 nnmaildir을 이용해서 읽는 것을 시도해 봤는데 만족스럽지가 않다. 생각과는 달리 Gnus의 nnmaildir backend가  nnimap보다 빠르지 않다는 newsgroup의 글들이 검색이 된다. Fetchmail + procmail을 통해 imap에서 메일을 읽어서 local dovecat IMAP 서버로 서비스하는 식으로 사용하는 사례와 만족한다는 글이 있다.

- Mew에서는 maildir folder를 내부 관리용으로는 사용하는데 maildir를 접근할수 없다는 글이
  있다. maildir folder를 사용하는 것이 대안이 될 수 없는가? Mew로 IMAP folder 접근하는 것도
  체감속도가 빠르지 않다.

- Gnus와 Thunderbird, Apple Mail을 잘 조합해서 써야겠다

- [2010-08-16 Mon] 최근에는 Gnus에서 메일은 가끔 write하기 위한 용도로만 사용한다. Mac에서 Gmail과 [mailplane client](http://mailplaneapp.com/)를 이용하는 방식으로 변경했다. Gmail의 spam filtering, label, 검색 기능이 주는 잇점에 만족하고 있다.


