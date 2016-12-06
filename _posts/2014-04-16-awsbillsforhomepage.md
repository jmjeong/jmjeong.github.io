---
layout: single
title: AWS 과금 내역 - 로그 Tracking 용
description: 
category: 
tags: aws
---

## 2014. 8월 : $1.24

## 2014. 7월 : $1.53

## 2014. 6월 : $1.34

## 2014. 5월 : $0.92

- CloudFront : $0.36
- Route 53 : $0.51
- S3 : $0.05

## 2014. 4월 : $0.85

- CloudFront : $0.28
- Route 53 : $0.51
- S3 : $0.06

## 2014. 3월 : $1.21

- CloudFront : $0.15
- Route 53 : $1.01
- Simple Storage Service : $0.05 

CloudFront는 각 Region별로 별도 계산되어 합산이 되고, Requests가 1번이라도 되면 최소 비용이 $0.01이
부가된다. 그래서 한번이라도 접근이 있으면 각 region별로 최소 비용이 $0.03씩되어서 5개 region이면
$0.15가 된다.

Route 53은 hosted zone당 $0.5 기본에 1,000,000 query 당 $0.5인데 최소 비용으로 $0.01이 부가되었다.
Route 53은 테스트를 하느라 hosted zone을 하나 더 만들어서 $0.5가 더 과금되었다.
