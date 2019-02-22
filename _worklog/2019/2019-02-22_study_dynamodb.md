# dynamodb(DDB)



latency 주력(일관된성능 발휘)
돈낸만큼 성능발휘
  이지만 throttling 발생..(성능지연X -> 요청거부)

insert가 몰릴때를 대비해 fluentd와같은 버퍼를 두는게 좋겠다

kafka로 밀어거나 app에서 connection 붙어서 쏴대면 힘들어할 것 같다.

queue 형태아키텍처를 잡아야 효율적으로 사용가능

## 요금
https://aws.amazon.com/dynamodb/pricing/

### Pricing for on-demand capacity mode
ondemand 요금은 쓴만큼 내지만

### Pricing for provisioned capacity mode
읽기/쓰기 처리량 계산해서 미리 구매

잘 이해 안가는데...

단위는 1 트랜잭션으로 봐야할 것 같다
RCU 읽기파워 up to 2kb
 - strongly consistent read per second

WCU 쓰기파워 up to 1kb

```
Monthly Commitment 	Upfront: 1-Year 	Hourly: 1-Year 	Upfront: 3-Year 	Hourly: 3-Year
100 Write Capacity Units 	$162.83 	$0.014 per Hour 	$195.32 	$0.0088 per Hour
100 Read Capacity Units 	$32.49 	$0.0028 per Hour 	$38.95 	$0.0017 per Hour
```
100 WCU - 예약 1년 160달라, 3년 195달라
100 RCU - 예약 1년 32달라, 3년 38달라
3년 예약하라는거네





