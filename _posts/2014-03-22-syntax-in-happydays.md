---
layout: post
title: Syntax used in HappyDays
description: 
category: [happydays,ios]
tags: happydays ios
image:
  teaser: t-happydays-3.jpg
---

#### Syntax

    title,date[d-day]

- `title` and `[d-day]` is optional
- date format of `date` follows date format  in Setting of HappyDays
- lunar date starts with '-'
- `/`, `.`, and `-` can be used for delimiter of date
- `d-day` can be positive and negative
  - the number with prefix `+` and `-` **don't** include event day for calculation
  - the number without prefix `+`, `-` **do** include event day for calculation
- date **with** year field having d-day specifies only one day
- date **without** year field having d-day specifies the repetitive days

#### Example

	10/9
	New year,1/1
	New year in lunar,-1/1
	ThanksGiving in lunar,-8/15
	John birthday,2010/5/3
	100th event since I met her,2014/3/1[100]
	100th day after a baby is born,2014/1/1[100]
	The day after new year,1/1[+1]
	The day before new year,1/1[-1]
	The 50th day before the exam,2014/11/10[-50]
	Christmas in 2014 only,2014/12/25[0]

