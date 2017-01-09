---
layout: post
title: amazon lightsail 잠깐 사용기
description: 
category: 
tags: amazon, lightsail, aws
---

개발용 jira, confluence를 설치해서 사용하는 EC2가 메모리가 여유롭지 않아 amazon lightsail로 이전을 시도해 보았다. VPS이지만 예측 가능한 가격과 저렴한 데이타 전송 요금이 매력적이었다. 

메모리 부족 문제인지, virginia로의 네트웍 문제인지, 아니면 VPS hosting 특성인지, SSH 접속이 안 될 정도로 느려지는 경우가 발생해서 문제가 발생하여 당분간 사용하지 않기로 결정했다. 잠깐 테스트 목적으로는 괜찮은 것 같은데 서비스를 올리기엔 안정적이지 않아 보인다. 

## $20/month plan

 **2GB RAM, 1vCPU, 40GB SSD, 3TB data transfer**

confluence가 메모리 부족으로 뜨지 않는 문제가 생겼다. 공동 편집 목적의 `synchrony`의 할당 메모리가 1G이다 보니, 최소 메모리 요구량이 2G가 넘는다. 

## $40/month plan 

**4GB RAM, 2 vCPUs, 60GB SSD, 4TB data transfer**

jira, confluence 모두 잘 구동되었다. Virginia region이라 한국에서 접속이 약간 느린 감은 있었지만, 테스트 목적으로는 문제가 없어 보였다. Host로 접속을 하지 않다가 다시 접속하는 경우 접속이 잘 안 되는 경우가 보인다. (*사용하지 않기로 결정*)

