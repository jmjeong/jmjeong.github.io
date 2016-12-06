---
layout: post
title: Ubuntu에 Gitosis Install
description: 
category: 
tags: git 
---

## gitosis package  install

    sudo apt-get install gitosis

Install package가 gitosis 계정을 자동으로 만들어준다. 긴 이름 대신에 짧은 이름이 낫기 때문에 
gitosis 계정 대신 git 로 변경한다. git 계정은 passwd는 필요하지 않지만, 유효한 shell을 가져야만
로긴이 된다. 

    sudo vi /etc/passwd/ /etc/group 
    pwconv && grpconv

gitosis를 관리한 *local host* 에서 ssh-keygen을 이용하여 public SSH를 key를 등록한다. 

    ssh-keygen -t rsa

$HOME/.ssh/id\\<sub>rsa.pub</sub> 파일을 gitosis가 *운영될 서버* 로 copy한다.

public SSH key를 authorized key로 등록한다. 

    jmjeong@jmhost:/srv/gitosis$ sudo -H -u git gitosis-init < /tmp/id_rsa.pub 
    Initialized empty Git repository in /srv/gitosis/repositories/gitosis-admin.git/
    Reinitialized existing Git repository in /srv/gitosis/repositories/gitosis-admin.git/

*local host* 에서 gitosis가 운영 중인 admin 파일을 받아온다.

    jmlocal:~ jmjeong$ git clone git@YOUR_SERVER_HOSTNAME:gitosis-admin.git 
    Initialized empty Git repository in /Users/jmjeong/gitosis-admin.git/.git/
    remote: Counting objects: 5, done.
    Receiving objects: 100% (5/5), done./4)Receiving objects:  20% (1/5)   
    Resolving deltas: 100% (1/1), done.
    remote: Compressing objects: 100% (4/4), done.
    remote: Total 5 (delta 1), reused 5 (delta 1)

## 새로운 repository를 만들기

*gitosis.conf* 를 열어 보면 아래와 같은 default 값이 설정되어 있다. 

    [gitosis]
    
    [group gitosis-admin]
    writable = gitosis-admin
    members = jmjeong@jaemok-jeongyi-macbook-pro.local 

*gitosis.conf* 에 새로운 group을 생성한다.

private group 이름은 다른 이름이나 상관없고, 이 그룹에 속해 있는 사람은 *journal* 이라는 repository에 대해
write 권한을 가진다.

    [group private]
    members = jmjeong@jaemok-jeongyi-macbook-pro.local
    writable = journal
    
    [repo journal]
    description = Jaemok's journal
    owner = jmjeong@jaemok-jeongyi-macbook-pro.local

*john* 이라는 사람이 journal이라는 repository에 readonly access 권한을 주고 싶은 경우에는 아래와 같이
설정이 가능하다.

    [group private-ro]
    members = john
    readonly = journal

설정을 마친 후에는 commit & push 한다. 

    git commit -am "Create journal repository & grant jmjeong to write journal"
    git push 

## 새로운 user 등록

    ssh-keygen -t rsa

명령어로 key를 생성한 후, `id_rsa.pub` key를 keydir로 copy한 후 add, commit 한 후 서버로 push한다. 
이 때 파일 이름을 `id_rsa.pub` 내에 있는 user 이름으로 하고, 그 뒤에 확장자를 꼭 \*.pub\*로 해야 한다.
확장자를 맞춰주지 않는 경우에는 server의 gitosis-admin repository의 keydir에 key가 등록이 되었는데도
불구하고, ssh 접속 권한이 열리지 않는 문제가 생긴다. <span class="timestamp-wrapper"><span class="timestamp">&lt;2010-08-16 Mon&gt;</span></span>

    jmjeong@jmjeong-ui-MacBook-Pro.local.pub
