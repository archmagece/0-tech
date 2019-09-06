BlockChain Developer
====================

## 목차

1. 블록체인&코인 기술
    1. Bitcoin
        1. Whitepaper
    2. Ethereum
    3. EOS
    4. IOTA
    5. Hyperledger fabric
    6. Hyperledger sawtooth
    7. 기타 기술
2. 블록체인 기반기술
    1. 암호화 알고리즘
        1. Keys
        2. ECC, Secp256k1
        3. Base58Check Encoding
        4. mnemonic
    2. 트랜잭션
        1. 알고리즘
        2. UTXO
        3. 트랜잭션 Structure
        4. Bitcoin Script
    3. 블록 생성
    4. 머클트리
    5. 블록체인 구현하기
3. 합의 알고리즘
    1. 트랜잭션의 유효성 검증
    2. 작업증명 POW
        1. 작업증명 목표값과 Difficulty
        2. 마이닝과 Hashrate
        3. 블록 유효성 검증 방법
        4. 6 Confirmation
        5. folk와 Consensus
        6. Confimation
    3. 지분증명 POS
        1. pos방식.
    4. 기타
4. Network
    1. 노드
        1. 기능과 종류
    2. SPV 노드와 Bloom Filter
    3. P2P, Relay network
    4. Network Message

## 블록체인&코인 기술

### 비트코인

#### 비트코인 백서

* 신용에 기반하지 않는 시스템
* 디지털 서명을 이용해서 소유권을 명확히 함
* 이중지불을 방지하기 위해 과반수의 컴퓨팅 파워를 사용하는 노드를 사용해 투표

#### 상세설명
노드 분포도
마이닝 풀 집중도
소스코드 주소
비트코인 캐시

비트코인의 구성요소
* 분산화된 P2P 네트워크 (비트코인 프로토콜)
* 공개거래장부 (블록체인)
* 분산화된 수학적 결정론적 통화 발생 (분산채굴)
* 분산화된 거래 검증 시스템 (거래 스크립트)
* Wallet

### 이더리움

비탈릭 부테린
비트코인은 지불과 소유권 이전(계약)의 이행을 확신할 수 없다
이더리움은 스마트컨트렉트를 통해 지불과 소유권의 이전을 동시에 진행 가능

이더리움 로드맵
1단계. 프론티어
2단계. 홈스테드
3단계. 메트로폴리스
4단계. 세레니티

Account
UTXO의 비효율성 해결
* nonce
* id - 트랜잭션 중복방지 카운터
* balance
* root
* codehash

* P2P Network
* Concensus rules
* Transactions
* State machine
* Data structure
* Economic security
* Clients

Gas price와 limit

### Hyperledger

그냥 메시지기반 서버 아키텍처
블록체인을 처리하는 시스템으로
분산형으로 처리하면 효율성이 떨어짐

디비에 저장하는 것보다 나은점은...
변조방지 정도의 효과만 있음


### 코인의 주요 개념

비잔틴 장군 문제
이중지불 문제
관리의 집중화 방지


## 블록체인 기반기술

암호화 알고리즘

hash
타원곡선암호화 ECC(Elliptic Curve Cryptography)
Scep256k1


libbitcoin 라이브러리
비트코인 어플리케이션 제작을 위한 크로스플랫폼 라이브러리

