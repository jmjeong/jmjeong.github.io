---
layout: post
title: Orgmode를 이용한 Blogging
description: 
category: 
tags: emacs
---

Emacs의 [orgmode](http://orgmode.org)는 노트, 스케줄 관리, 문서 저작등을 위한 major 모드이다.
Orgmode 기능 중에 하나인 export를 이용하면 작성한 문서를 latex, html, pdf등으로 변환할 수
있다. 개인적으로 회의록이나 일정, 생일, 메일등을 orgmode를 이용하여 관리를 하고 있다. Orgmode를 통해
홈페이지에도 글을 올릴 수 있으면 좋겠다는 생각을 했었고, 관련 solution에 대해서 고민을 해 보았다.

현재 운영 중인 홈페이지는 wiki로 되어 있다.Wiki는 간단한 문법으로 구성되어 있어 static html파일에
비해 문서 작성이 용이한 장점이 있다. 온라인상으로 페이지를 편집하고 글을 올리기 쉬운 장점과 함께,
브라우저의 edit 창을 통한 편집하고 올리는 것은 긴 글에는 적합하지 않다. (한동안 firefox의
[It's All Text!](https://addons.mozilla.org/en-US/firefox/addon/4125)
plugin을 시도했으나 역시 마우스 클릭 등이 필요해서 불편했다) 

Emacs를 통해서 블로그에 직접 글을 올리는 방법으로 몇가지 solution이 나와 있다(참조:
[Emacs를 통해서 blog 작성하기](http://aidi.tistory.com/entry/emacs-weblog-%EC%9D%B4%EC%9A%A9%ED%95%98%EA%B8%B0-2%ED%83%84-1))
막상 이런 solution을 사용해보면 뭔가 2% 부족함을 느끼게 된다.  개인적으로는 XML-RPC를 이용한 wiki
editing mode중에 가장 완성도 높은 것이
[TracWiki](http://jmjeong.com/index.php%3Fdisplay%3DEmacs/TracWiki)였다.

몇 년전부터 todo list에만 올려두고 미뤄왔던 홈페이지 개편 생각이, 최근 github에서 활용되는
[jekyll](http://github.com/mojombo/jekyll/tree/master)과 Ordmode의 [Worg](http://orgmode.org/worg/)
프로젝트를 보고 다시 고민을 하게 되었다. 특히 Worg는 git와 orgmode의 export를 통해 homepage가
운영되고 있다. 모든 페이지는 orgmode의 emacs document로 이루어져 있고, 주기적으로 git server로부터
내용을 pull한 다음에, emacs의 batch script를 이용해서 html로 변환하게 된다.

Worg가 원하는 기능의 많은 부분을 충족시키고 있지만 orgmode format, version control system을 통한
관리, 자동 index generation, customized page formatting등 부족한 부분이 있다.

필요로 하는 기능은 아래와 같다.

-   Orgmode format 유지
-   Git나 다른 vcs를 통해서 서버에 submit
-   자동으로 blog 형태로 html로 보여주는 interface
-   Source highligting
-   Category, Tag support
-   web 2.0의 feature를 필요에 따라 사용할 수 있을 것(rss, comment, trackback)

관련 솔루션으로 [Blorgit](http://orgmode.org/worg/blorgit.php),
[Jekyll](http://github.com/mojombo/jekyll/tree/master), Hyde, [Worg](http://orgmode.org/worg),
[Blogofile](http://blogofile.com)등을 검토하다가, 최종적으로 Blogofile에 org-markup 모듈을 추가하는
것으로 결론을 내렸다. 이 블로그는 blogofile을 통해서 orgmode로 작성된 text를 변환하여 만들어진다.

작성된 'orgmode mark up for posts' 기능은 원 저자에게 보내져서 0.5 버젼에 반영이 되었다.

### 참고로 읽어볼만한 글

-   <http://zegoggl.es/2009/05/jekyll-vs-marley.html>
-   <http://metajack.im/2009/01/23/blogging-with-git-emacs-and-jekyll/>
-   <http://biodegradablegeek.com/2009/03/how-to-maintain-static-sites-with-git-jekyll/>
-   <http://matflores.com/2009/04/28/using-git-to-maintain-your-blog.html>

### 고려할 점

-   Syntax highlighting Color
-   Speed benchmark
-   Embedded Latex fragment 지원
-   Ditta, Gnuplot등 외부 모듈 검토 지원
-   TODO 관리

---

홈페이지 서버를 교체하면서 blogofile+orgmode extension Blogging을 2주 정도 사용 중이다. 
느낀 점을 간단히 정리하자면&#x2026;

-   기대했던 것처럼, html browser 대신에 emacs을 사용할 수 있고, 익숙한 orgmode에서 사용할 수 있다는
    측면에서 매우 편하다

#### 불편한 점

Blogofile + orgmode extension 자체 solution은 현재로서는 쓸만한데, 글이 좀 많아지는 경우에는
몇가지 문제가 생길 수 있다

-   Orgmode article -> html 변환 시, emacs와 orgmode의 변환에 따라 다른 결과물이 나온다.  특히
    orgmode이 version-up함에 따라 formatting 결과가 다르게 된다. 또한 매번 변환을 emacs launch하여
    batch로 처리가 되다보니 글이 많아지면 속도가 문제가 된다. 처음 검토했을때 각 글당 1초 미만으로
    걸리고, 서버측에서 자동으로 처리가 되는 부분이니 무시해도 되지 않을까 생각했던 부분이다
-   Syntax highlight 처리 : orgmode에서는 자동으로 처리가 되었는데 batch로 처리를 하니 색 지정이
    되지 않고 face 처리가 된다
-   [Org babel](http://orgmode.org/worg/org-contrib/babel/org-babel.php) : latex fragment, ditaa 등을 고려하면 최종적으로 검토를 해야 하는데, 이 부분을
    서버측에서 처리를 하다보면 속도나 호환성 쪽에서 문제가 되지 않을까 하는 우려가 있다
-   문서의 update time : Blog article의 lifetime과는 달리 기존의 wiki처럼 문서를 만들어 놓고 계속
    수정 또는 첨가 형태로 운영을 하게 되는데, 각 article들의 update time과 페이지 상의 위치는 어떻게
    유지할까?
    -   yasnippet와 emacs write hook을 사용하는 대안 :
        yasnippet용 script로 [yaml](http://github.com/jmjeong/my-dot-emacs/blob/master/snippets/org-mode/yaml)을 정의하고, yaml이 blogofile용 header를 입력하게 하고, org mode에서
        파일이 저장될 때 `updated:` 항목을 갱신하는 방법으로 update를 변경하는 방법 : 페이지 자체에
        불필요한 정보가 들어있다 보니 orgmode exporter가 처리가 안 되는 문제가 있다. 

            (add-hook 'org-mode-hook
                      (lambda ()
                        (org-set-local 'yas/trigger-key  [tab])
                        (define-key yas/keymap [tab] 'yas/next-field-group)
                        (auto-fill-mode)
                        (add-hook 'local-write-file-hooks 'blog-updated-timestamp)
                        ))
            
            (defun blog-updated-timestamp ()
              "Upate blog-updated-timestamp"
              (save-excursion
                (goto-char (point-min))
                (let ((state buffer-read-only))
                  (when state (setq buffer-read-only nil))
                  (if (search-forward-regexp "^updated:" nil t)
                      (let ((beg (match-end 0)))
                        (end-of-line)
                        (delete-region beg (point))
                        (goto-char (match-end 0))
                        (kill-line)
                        (insert (format-time-string " %Y/%02m/%02d %02H:%02M:%02S\n" (current-time)))
                        )
                    )
                  (when state (setq buffer-read-only t)))))

### 개선점

-   HTML 변환을 org-publish에 의해 처리하고, 변환된 HTML에 yaml header를 붙여서 blogofile로 처리하는
    형태로 변환을 완료했다. F5를 눌러 현재 홈페이지에 올려진 각 article들을 살펴보고, 문서를 작성 후,
    F6을 누르면 자동으로 org-publish & blogofile 변환 작업을 하도록 작업 프로세스를 변경했다.

---

[Blogofile](http://www.blogofile.com/)은 [Jekyll](http://github.com/mojombo/jekyll)에 의해 영감을
받아 만들어진 스태틱 파일 블로그 엔진/컴파일러이다. PHP나 PERL등의 CGI script도 필요없고, mysql이나
sqlite3등의 database도 필요하지 않다. 모든 content는 HTML 형태로 서버에 저장이 되기 때문에, HTTP
서버만 있으면 구동이 가능하다. 또한 동적처리가 서버에서 이루어지지 않기 때문에 보안에 상대적으로
안전하다.

### 작업 환경

-   [Blogofile](http://blogofile.com) : static blog generator
-   [Emacs](http://www.gnu.org/software/emacs/) : GNU Emacs 23.1.50.1
-   [Org-mode](http://orgmode.org) : Org-mode version 6.30

Orgmode가 html 변환을 담당하기 때문에 6.x 버젼으로 org version의 버젼을 일치시킬 필요가 있다. 
변환된 HTML로부터 title, date, update날짜등을 자동으로 추출해 내는데, 변환된 HTML의 format이 다른
경우에는 오동작을 일으킨다.

### 얻어지는 장점

-   Source include나 highlight에 대해 별다른 고민을 할 필요가 없이, `src` `tab`을 누르면 yaml에 의해
      확장된 `#+BEGIN_SRC` ... `#+END_SRC`가 표시된다
-   =C-c C-x f=를 누르면 Footenote mark가 표시되고, 자동으로 footnote를 편집할 수 있는 화면으로 바뀐다
-   Section이나 subsection을 웹으로 publish하고 싶지 않을 때 `C-c ;`를 누르면 COMMENT mark가 표시되고
    웹 publish 여부를 결정할 수 있다
-   Emacs에서 `F5`를 누르면 현재 blog에 posting된 모든 글이 dired mode로 표시된다. Dired의 목록 list는
    최근 update 순으로 sorting되어 표시되어, 최근 수정한 내역을 알아볼 수 있다. 또한 blog post
    article은 git에 의해 유지 관리가 되므로 각 file별 수정 내역을 확인할 수 있다
-   Web에 publish하기 전에 대략적인 output formating을 알아보고 싶은 경우에는 `C-c C-e b`를 통해 html
    변환 결과를 확인한다
-   Emacs에서 `F6`을 누르면 org -> html 변환, site generation을 수행하고, `F7`을 누르면 웹 사이트에
      자동으로 upload한다. 변환된 local 결과는 `http://localhost/8080` 으로 확인이 가능하다
-   굳이 web에 접속하지 않아도 local로 blog entry들을 확인 가능하고, 편집이 가능하다
-   테이블 편집에 대해 고민하지 않고, orgmode의 **훌륭한** 테이블 편집 모드를 사용한다
-   작성된 org 파일은 필요에 따라 txt나 latex format으로 변환하여 출력이 가능하다
-   Category는 orgmode의 tag를 이용하여 구현했다. 작성된 article의 tag를 변경하고 싶은 경우에는
    아무데서나 =C-c C-q=를 눌러 section의 tag를 변경하면 된다
-   최근 수정된 문서는 blog에서 첫 페이지에 올라오고, 문서의 처음 작성일은 문서의 마지막에 표시된다

