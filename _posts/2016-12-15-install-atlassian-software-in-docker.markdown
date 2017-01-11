---
layout: post
title: atlassian jira, conflunce를 docker를 이용하여 설치 
description: 
category: 
tags: docker atlassian 
---

**Ubuntu 16.04.01(Xenial) LTS에 docker를 이용하여 atlassian jira, confluence 설치하기**

# Docker Install

- [참고문서](https://docs.docker.com/engine/installation/linux/ubuntulinux/)

## Pre-requisite 

```sh
$ uname -r
4.4.0-45-generic
$ sudo apt-get update
$ sudo apt-get install apt-transport-https ca-certificates
$ sudo apt-key adv \
               --keyserver hkp://ha.pool.sks-keyservers.net:80 \
               --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
$ sudo echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main"  | sudo tee /etc/apt/sources.list.d/docker.list
$ sudo apt-get update
$ sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
```

## Install docker

```sh
$ sudo apt-get update
$ sudo apt-get install docker-engine
$ sudo service docker start
$ sudo docker run hello-world
```

# Install atlassian software 

## Make directory 

```sh
$ mkdir -p /data/docker/postgresql /data/docker/confluence /data/docker/jira
```

## Postgres

```sh
$ docker run --name postgresql -itd --restart always \
  --env 'DB_USER=user' --env 'DB_PASS=password' \
  --env 'DB_NAME=jira,confluence' \
  --publish 15432:5432 \
  --volume /data/docker/postgresql:/var/lib/postgresql \
  sameersbn/postgresql:latest
```  

## Atlassian-Jira-Software

```sh
docker run --name jira -itd --restart always \
  --env 'JVM_MAXIMUM_MEMORY=1G' \
  --publish 18080:8080 \
  --volume /data/docker/jira:/var/atlassian/jira \
  cptactionhank/atlassian-jira-software
```

## Atlassian-Confluence

```sh
docker run --name confluence -itd --restart always \
  --env 'JVM_MAXIMUM_MEMORY=1G' \
  --publish 18090:8090 \
  --volume /data/docker/confluence:/var/atlassian/confluence \
  cptactionhank/atlassian-confluence
```

# 기타

- License issue로 인해 prebuilt docker image가 openjdk:8 을 base image로 사용 
    - atlassian software에서는 openjdk가 검증되지 않았다고 warning 메시지를 출력
    - Oracle Java installer로 변경하는게 나을 수도 - `sudo apt-get -y install oracle-java8-installer`
- 데이타 백업이 필요할 때  /data/docker directory만 복사하면 됨
- Jira, Confluence database 설정 
    - PostgreSQL
    - `jdbc:postgresql://<hostip>:15432/<confluence, jira>`
- docker shell 접속
    - `docker exec -it jira /bin/bash`

