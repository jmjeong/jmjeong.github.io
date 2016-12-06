---
layout: post
title: git 작업 결과 공유하기
description: 
category: 
tags: git
---

Git는 분산서버이므로 중앙집중 서버를 필요로 하지 않는다. 
Sync하고 있는 remote server가 죽더라도, 현재 local copy본에서 serve할 수도 있고, 
별도 backup본을 만들 수 있다. 

    git clone --bare ~/Dev/proj proj.git

저장된 `proj.git`를 서버에 올려두고 공유할 수 도 있고, 다른 machine에 복사하여
사용할 수 있다. 

    $ mkdir proj
    $ mv proj.git proj/.git
    $ cd proj
    $ git init
    Reinitialized existing Git repository in /Users/jmjeong/proj/.git/
    $ git checkout -f

해당 directory에서 `git-daemon`을 이용하여 `git://` protocol로 서비스 할 수도 있다.
