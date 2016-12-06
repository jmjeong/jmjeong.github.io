---
layout: post
title: RamNode 등록
description: 
category: 
tags: 지름
---

Intel E5 (2.3Ghz+) CPU, 1Gbps connection, 1 IPv5, 50GB Storage, 128MB RAM, 128MB VSwap,500GB
Bandwidth의 VPS 서비스를 40% 할인해서 1년에 $14.4에 판매를 했다. 아마존 EC2 Free Tier와 비교하면
메모리는 부족하긴 하지만, CPU 성능은 훨씬 낫다.  거기다가 500GB까지는 Traffic 비용이 들지 않는다.VPN
서비스 대용이나, FTP, BTSync의 원격 서버용으로 쓰면 괜찮을 듯 싶다.

- [http://www.ramnode.com/index.php](http://www.ramnode.com/index.php)
- [http://www.clien.net/cs2/bbs/board.php?bo_table=use&wr_id=611732](http://www.clien.net/cs2/bbs/board.php?bo_table=use&wr_id=611732)
- [http://www.clien.net/cs2/bbs/board.php?bo_table=lecture&wr_id=216634](http://www.clien.net/cs2/bbs/board.php?bo_table=lecture&wr_id=216634)

# Comments

간단한 웹 서버 정도 돌리는 용도로 괜찮을 듯 싶었으나, 조금만 메모리가 넘어가도 프로세스가
죽는다. cpan 명령으로 perl module을 몇개 설치하려고 했는데 설치할수 있는 방법이
없다. apt-get으로 package를 설치하는 경우에도 자주 죽는다. swap 파일을 만들어서 메모리를 늘려보려
했는데 이것도 막아 놓았다. [2014-04-17 Thu]
  
```sh
# dd if=/dev/zero of=/swapfile bs=1024 count=8192
# mkswap /swapfile
# swapon /swapfile
  swapon: /swapfile: swapon failed: Operation not permitted
```

- VPN Server를 설정해서 사용하니 속도가 1Mbps 나온다. [2014-05-14 Wed]
- arq 4라는 mac program을 구입 후, 사진 bakcup용으로 sftp 설정해서 사용 중 [2014-08-04 Mon]
- [https://www.digitalocean.com/pricing](https://www.digitalocean.com/pricing) 도 검토 
