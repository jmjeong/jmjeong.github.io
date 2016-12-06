---
title: appsales to graphite
layout: single
tags: node
category: node
---

Apple sales data를 graphite에 populate하는 node script 

[Source](https://github.com/jmjeong/appsales2graphite)

## Installation

```js
$ npm install

$ node index.js
$ pm2 start sales-watch.js
```

## Graphite에 전송된 값

- `app.<SKU>.<Type>.<Country>`

![](http://dr.jmjeong.com/1b4DQ+)

## Script

- index.js : `data_dir`에 저장되어 있는 S_D_로 시작하는 내용을 읽어서 graphite로 전송한다. 
- sales-watch.js : `data_dir`에 새로운 파일이 추가되면 graphite로 전송한다 

## App Sales data

iTunesStore에서 download 받은 sales data가 nemus-sales-data에 저장되어 있다. 

매일 sales data를 자동으로 download 받기 위해서 [Script](https://github.com/jmjeong/django-appsales/blob/master/sales/jobs/download.py)를 사용한다. 

```sh
...
-rw-r--r--  1 jmjeong jmjeong 14113 2014-01-02 00:00 S_D_12-31-2013.txt
-rw-r--r--  1 jmjeong jmjeong 11207 2015-01-02 00:00 S_D_12-31-2014.txt
-rw-r--r--  1 jmjeong jmjeong 18184 2016-01-02 00:00 S_D_12-31-2015.txt
...
```

