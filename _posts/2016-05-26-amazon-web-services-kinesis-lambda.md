---
layout: post
title: AWS Kinesis, API Gateway, Lambda
description: AWS Kinesis, API Gateway, Lambda
category: node
excerpt: AWS Kinesis, API Gateway, Lambda
tags: node, aws, amazon
---

- [PDF format](http://dr.jmjeong.com/1dNdw+)

# AWS Kinesis 장점

- 실시간
- 사용 편의성
- 병렬 처리
- 탄력성 - 확장 가능 
- 저렴한 비용 - 0.015 USD/h, 1M/sec
- 안정성 - AWS 리전 3개 시설에 복제

---

# 사용 사례

- 로그 및 이벤트 데이터 수집
- 모바일 데이타 캡처
- 실시간 분석
- 게임 데이타 피드


---

![fit](https://d0.awsstatic.com/amazonkinesis/kinesis-architecture-crop.png)

---

# 요금

- 샤드 시간 base로 청구
- 샤드 1개 초당 1MB의 데이터 입력 및 2MB의 데이터 출력 용량 제공
- 샤드 1개 초당 1000개의 레코드 지원 
- 기본 보관 - 24시간
- 가격 : 샤드 시간(초당 1MB 수신, 초당 2MB 송신) - **$0.015**/h

---

# AWS API Gateway

---

어떤 규모에서든 개발자가 API를 손쉽게 생성, 게시, 유지관리, 모니터링 및 보안할 수 있는 해주는 완전 관리형 서비스

- 트래픽 관리
- 권한 부여 및 액서스 제어
- 모니터링
- API 버전 관리

---

![fit](https://d0.awsstatic.com/products/APIGateway/API_Call_Flow_v2.jpg)

---

# 장점

- 낮은 비용과 효율성
- 어떤 규모에서도 뛰어난 성능
- API 작업을 간편하게 모니터링
- API 개발 간소화
- 유연한 보안 제어
- 기존 서비스를 위한 Restful 엔드포인트 생성
- 서버 없이 API 실행

---

# 요금

- 수신된 1백만 API 호출당 3.50 USD
- 기가바이트 데이타 전송 비용 추가
  - 처음 10TB에 대해 0.09 USD/GB
- 캐시 메모리 크기 별 과금
  - 0.5GB - 0.020 USD

---

# Lambda

---

이벤트에 응답하여 코드를 실행하고 자동으로 기본 컴퓨터 리소스를 관리하는 서버 없는 컴퓨팅 리소스

- 커스텀 로직으로 다른 AWS 서비스 확장
- 커스텀 백엔드 서비스 구축
- 완전히 자동화된 관리
- 내결함성 기본 제공
- 자동 조정
- 통합된 보안 모델
- 자체 코드 사용 가능

---

# 요금

- 요청
  - 매월 첫 요청 1백만 회까지 무료
  - 이후 요청 1백만 회당 0.20 USD
- 기간
  - 사용한 매 GB-초당 0.00001667 USD

---

# Example

```javascript
console.log('Loading function');

exports.handler = function(event, context) {
    console.log('event:', JSON.stringify(event));
    var name = event.myname || 'Anonymous';
    context.succeed('Hello World, '+name);
};
```

---

# Invocation

- Using Event Sources such as Amazon S3, Echo, DynamoDB, SNS, and etc
- On-demand Lambda Function Invocation: Over HTTPS
- On-demand Lambda Function Invocation: Building your Own Event Sources

---

# Programming Model


- Node.js, Java, Python

- Handler
- Context object
- Logging
- Exceptions

---

# Node.js

- runtime v4.3
- runtime 0.10.42 (will be deprecated in October 2016)

---

# Handler

```javascript
exports.myHandler = function(event, context, callback) {
   console.log("value1 = " + event.key1);
   console.log("value2 = " + event.key2);  
   callback(null, "some success message");
   // or 
   // callback("some error type"); 
}
``` 

- event - event data
- context - runtime information
- callback - return information to the caller

---

# Logging

- console.log()
- console.error()
- console.warn()
- console.info()

---

# Exceptions

```javascript
console.log('Loading function');

exports.handler = function(event, context, callback) {
    // This example code only throws error. 
    var error = new Error("something is wrong");
    callback(error);
   
};
```


---

# Best Practices

- Write your lambda function code in stateless style
- Avoid declaring any function variables outside the scope of handler
- Make sure you have set `+rx` permissions on your files in the uploaded ZIP
- Lower costs and improve performance by minimizing the use of start up code
- Use the built-in CloudWatch monitoring of your lambda function to view and optimize request
latencies
- Delete old Lambda functions that you are no longer using


