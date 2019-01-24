# 백엔드 개발조직

## 개발목표 서비스

### 서비스별 기술스텍

#### Block Chain Service

* ERC20서비스 및 기타 관련서비스
* ex) crypto kitty, 3piks, ...
* TechStack - BlockChain Wallet, BackendServer
* ...

#### Margin Trading

* 분산형 거래소(DEX) or 중앙형 거래소(Bittrex,Upbit,Binance)
* ex) bitmex
* TechStack
  * ##추가인력###아키텍트 항목
  * 서버로그 - 서버로그
  * 거래로그 - 이상행동감지

사용자가 기존업체의 완성된 서비스만큼의 성능과 보안, 속도, 안정성을 기대

##### 프로토타이핑

**CloudNative(AWS)**\
AWS 서비스 활용. 비용이나 기타 문제되는 부분은 차후 변경\
API GW, S3, EKS, RedShift, SQS, DynamoDB ...

* bitmex 서비스 참고
* reactive server API - 서버언어 KotlinOnSpring으로 시작
* Docker Container 기반 개발/배포/운영

#### AI & ALGO Trading

* 세부적인 서비스 종류에 따라 ..
* ex) ???
* TechStack - ???

## 개발스타일

1. CloudNative - 클라우드활용 극대화(AWS의존성 커지더라도 빠르게 효율적으로) - AWS스터디 비용은 필요
   * DynamoDB
   * AWS GW
   * ELK(Kubernetes on AWS)
2. DevOps
   * CI/CD 테스트-배포 자동화
3. SpringBackend
   * KotlinOnSpring 중심
   * 타 언어 및 프레임웍 필요한 곳에 사용

## 기술스텍

### 보안

???

* DDOS 방어
* 소스코드 단계에서의 보안코딩(일반적인 보안규정)
* 개인정보 관리(중요정보 암호화)
* 개인인증 - OPT, OAuth, Social ..
* API인증 - JWT

### 블록체인 지갑개발

Coin Wallet - 모든 Coin은 Wallet이 있는데 해당 코인상장을 위해서는 Wallet에 대한 분석 필요

* Bitcoin - C++
* Ethereum - golang
* Arc - TypeScript
* ...

Wallet 사용방법

* Wallet Daemon API호출 or 지갑데몬을 서버에 추가
  * 몇 가지 테스트 및 스터디 필요
  * Wallet Daemon의 수용가능 한계 확인
  * 분산형으로 호출이 가능할지 확인
  * 문제점: API호출이 아닌 별도 서버개발의 경우 속도개선은 있을 수 있으나 버전업데이트를 못 따라갈 가능성
* bit-go 등 거래소 지갑 솔루션과의 연동
  * 지원기능 확인

### 블록체인 네트워크 별도 개발

* ???

https://www.coindesk.com/blockchain-application-stack

* Network
* Decentralized Protocol
* BlockChain

### Backend

* Server Main
  * Spring, Kotlin
* Server Sub
  * Java, Scala, Groovy는 서브언어 Clojure는 참고
  * Node(TypeScript)...js 지양
* DB,Domain
  * JPA
  * RDBMS - mysql, ...
  * NoSQL - Cassandra, DynamoDB ...
* Script
  * Python, Ruby ...
* Infra as Code
  * Ansible ... 유사기술 Chef, SaltStack ...
  * Bash
* Container
  * Docker
  * Kubernetes
* DevOps
  * Jenkins, Docker, Maven, Gradle, TDD
* MSA
  * MSA개발기술 netflix style - Zuul, Ribbon, Eureka, Histrix...
* Cache
  * Ehcache, Memcached, Redis, ...
* MessageQueue - Kafka, RabbitMQ
* MessageProtocol - Protocol Buffer, JSON, BSON
* API호출프로토콜 - gRPC 또는 kafka이용. 또는 http2... 검토필요

### Frontend

* Language: TypeScript 중심, .... clojurescript, kotlinscript. ..
* Framework: vue(... react, angular) ... flutter
* Build: webpack, grunt, gulp
* Markup: CSS, SCSS, SASS, HTML

## 추가인력

### 개발환경 통일 - mac OSx

* Docker Container 기반 환경 구성에 편리. 윈도우 사용시 가상환경 필요.
* 개개인이 발생하는 이슈를 알아서 처리할 수 있는 경우에 한해서 OSx, 윈도우, 리눅스 혼합환경이 가능
* 신규 업무인력 스크립트를 이용해서 상당부분 개발환경 자동셋팅 가능

### 교육필요한 부분

* git branch 활용전략
  * 선행지식 필요없음
  * 기간 1~2일
* spring framework
  * 선행지식 객체지향, 자바, 코틀린, JVM, 스프링프레임웍
  * 기간 3개월
* 코드리뷰 방법
* 내부 개발 프로세스
* 서비스 구조
* 도큐먼트 관리 - 업무지식 위키
* 서비스별 선행지식 정리

### 아키텍트

웹페이지 수준의 서비스인 경우 불필요

백엔드 개발자 1~2인으로 가능

대규모 서비스인 경우 아키텍트역할필요\
(거래소, 대규모서비스, 환성된 DevOps환경)

```text
ex) upbit, bithumb
kotbit, bithumb 서버 맨날 터지는 이유 - 설계 실패
관련기술 및 경험 :
MSA, Cloud(GCP,AWS,Azure), Container
분산형 서비스 - scale out, transaction, kubernetes, orchestration
0.000000000001단위 계산오차손실고려
지갑 보안 - bitgo 솔루션, 별도개발
로그인 보안 opt... 추가인증 프로세스
ddos 방어 - 솔루션 사용 및 직접 처리
로깅, 모니터링, 데이터분석, 이상감지
```

### 주니어 투입

개발 프로세스가 어느정도 완성팀에만 투입 가능

* 교육과 업무 병행가능한 인원구성
* 시니어1 : 주니어3
* 코드리뷰, 기술스터디
