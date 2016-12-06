---
layout: post
title: Sublime Text 3
description:
tags: mac
category: mac
image:
  teaser: t-sublime-text.jpg
---

Emacs 24가 shift-space로 한영 전환에 문제가 있어서 23.4를 사용하고 있는데,
가끔 사용 메모리가 Giga 단위로 늘어나는 문제가 있어 Sublime Text 3 에디터를 테스트 해 보았다.
$70으로 다른 에디터에 비해서 다소 비싸지만, 지속적으로 업데이트가 되는 점이나
[라이센스 정책](http://www.sublimetext.com/sales_faq)이 마음에 들었다.

- 멀티 OS, 컴퓨터 사용 가능 : 한번 구입으로 mac, linux, windows 버전 사용 가능
- 개인용 라이센스로 업무용 사용 가능
- Evaluation version이 가끔 구매 popup이 뜨는 것을 제외하고는 별다른 time limit가 없음

에디터 내에 package 관리자가 내장되어 snippet나 syntax, theme을 인스톨할 수 있고, python으로 
package를 제작할 수 있는 것도 매력적이다. 폰트나 탭 크기 등 각 설정들은 json 파일로 관리된다. 

![](https://farm6.staticflickr.com/5576/14670288241_fe5172a69e.jpg)

10M 이상의 큰 파일을 열어서 편집할 때도 괜찮은 속도를 보여주고, IDE 처럼 symbol을 참조하거나 문서를
볼 수 있는 기능도 있다. 사용자 층이 많아서 인터넷 상에 관련 자료가 꽤 있다.

어느정도 생태계가 구축되어서 설정 파일을 백업해서 공유해주는 [서비스](https://sublimall.org/)와
완성도 있는 [유료 플러그인](https://sublimegit.net)도 판매되고 있다.

### 키 리매핑

Emacs에서 사용했던 바인딩대로 meta+f, meta+b로 단어 단위 이동과 meta+g를 누르면 escape로 동작하도록
조정했다.

{% highlight json %}
[
    { "keys": ["super+k", "super+l"], "command": "set_mark" },
    { "keys": ["ctrl+g"], "command": "show_overlay", "args": {"overlay": "goto", "text": ":"} },

    // redefine word movement
    { "keys": ["super+b"], "command": "move", "args": {"by": "subwords", "forward": false} },
    { "keys": ["super+f"], "command": "move", "args": {"by": "subword_ends", "forward": true} },
    { "keys": ["super+shift+b"], "command": "move", "args": {"by": "subwords", "forward": false, "extend": true} },
    { "keys": ["super+shift+f"], "command": "move", "args": {"by": "subword_ends", "forward": true, "extend": true} },

    // redefine find command 
    { "keys": ["ctrl+super+f"], "command": "show_panel", "args": {"panel": "find", "reverse": false} },

    // cancel for super+g
    { "keys": ["super+g"], "command": "hide_panel", "args": {"cancel": true},
        "context":
        [
            { "key": "panel_visible", "operator": "equal", "operand": true }
        ]
    },

    // Rebind "go to file" to cmd+shift+O
    { "keys": ["super+shift+o"], "command": "show_overlay", "args": {
        "overlay": "goto",
        "show_files": true
    }},
]
{% endhighlight %}

#### 매뉴얼에 나오지 않는 기본 키

- 현재 커서 밑의 글자 지우기 : Ctl-D
- 파일 제일 앞으로 이동 : Cmd-Up
- 파일 맨 마지막으로 이동 : Cmd-Down


#### 설치한 package

- Anaconda : python ide
- Better close Window : 윈도우 창을 닫을 때 project를 save
- Git gutter-Edge : git 관리되는 파일 들에 대해서 수정된 라인을 표시 
- SublimeGit : 상용. magit와 비슷한 기능을 가진 git plugin. 기능이 뛰어나다 
- SublimeREPL : node, python 인터프리터를 수행하기 위한 package
- Quick File Open
- SideBarEnhancements

- Dayle Rees Color Theme

### Emacs와 비교 

- pgp, newsreader, mail, tramp, orgmode, magit 등 다양하고 powerful한 package에 비할바는 아니지만
  나름대로의 package를 갖추고 있다.
- 설정 파일이 json을 사용해서 직관적이긴 하지만, emacs의 `describe-key`, `describe-function`등의
  기능이 아쉬웠다.
- [python을 사용한 package system](http://www.sublimetext.com/blog/articles/choosing-an-extension-language)은 
    elisp와 같은 확장 가능성이 있어 보인다. Emacs의 magit와 유사한 SublimeGit도 완성도가 높다. 
- Emacs보다 화면 그리는 속도나 loading 속도가 빠른 점은 맘에 들었다. 
- sublime text 3의 [package 웹 사이트](https://sublime.wbond.net)나 인터페이스가 [elpa](http://tromey.com/elpa/)보다 낫다. 

### 기타

- Undo시 이상동작 : 한글이 들어가 있으면 undo 동작이 이상하다

>> ![](http://cl.ly/image/2d34151Q3v1I/sublime-hangul-undo.gif)

- 입력기와 충돌인지 아니면 설치된 package와의 충돌인지 모르겠지만 shift-space로 한영 전환이 안 되는
  경우가 있다.

- Preferences에서 설정을 바꾸고 나면 프로그램을 재시작해야지만 동작한다. Reload 설정이 있을 것 같은데
  못 찾겠다.

- Sublime Text 3 베타 마지막 릴리즈가 2013. 12월이다. Forum을 살펴보니 개발이 진행되고 있으나
내부적인 문제가 있는 듯 하다. Atom을 개발한 Github가 인수한다는 rumor도 잠깐 있었으나 포럼에서는
공식적으로 부인했다. 구입을 할까 하다가 정식 버전 나올 때까지 미루기로 했다.
