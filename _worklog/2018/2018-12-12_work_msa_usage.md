# msa book

API G/W - inner, outer

외부에서 접근하는 GW
내부API가 사용하는 GW 분리

외부API는 외부 인증코드 지원 JWT 등
내부GW는 고정키방식. 꼭 JWT를 써야 하는가 고민


kubernetes 와 같은 컨테이너클러스터를 활용하지 않으면 불가능.
serverless는 일부 기능을 대체할 수는 있으나 컨테이너가 필수

## api버전
* /latest/**
* /v20181130/**
* /v20181211/**

/latest 또는 특정 버전 지정 호출

/latest가 오류날 경우 지정버전호출

신규배포시에는 특정시점의 latest와 연동 테스트 실행

특정 버전 instance가 없는 경우 컨테이너 실행

## 로깅
모든 컨테이너에 fluentd 수집기 
로그수집 플랫폼 설치 연동
MS사이의 from-to logging

## CI/CD

## 무중단배포

## 설정값 보관
etcd ...

## CQRS
Command-Query Responsibility Segmentation

## 캐싱

### 클라이언트, 프록시, 서버캐싱
Redis, memcached, CDN

### http 캐싱
cache-control 캐싱 시간주기 지정 - 정적컨텐츠
Expires 헤더 - 새 버전의 데이터가 언제 업데이트 되는지 예상이 되는 경우

ETag(EntityTag) 리소스의 값이 변경되었음을 나타낸다
response에서 ETag:9jre40tji4t
를 받고
request에서 ETag:9jre40tji4t
를 보내면
304 Not Modified
새 버전이 있으면 새 ETag값과함께 200 OK

### 쓰기용 캐싱
write-behind : 일단 변경사항 저장해놓고 한꺼번에 수정


## CAP 정리theorm
일관성consistency
가용성availablity
분할용인partition tolerence

AP/CP/

## Service Discovery

### DNS

### 동적 서비스 레지스트리

zookeeper, consul, Eureka

## 문서화

swagger, HAL




Ribbon..로드밸런싱이기도 하지만


