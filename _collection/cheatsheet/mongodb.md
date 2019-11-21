# mongodb

## 단순검색
db.getCollection('votelists').find({voteDate: '2019-11-19', voteNumber: 15})

long 형태의 date 값을 formating
db.getCollection('votelists').find({voteDate: '2019-11-19', voteNumber: 15})
.forEach(function(a,b,c) {
  
})

print(new Date('2019-11-20T00:00.000Z').getTime(), new Date('2019-11-20T00:00Z').getTime(), new Date())


## 악질적인 데이터 검색

### 악질적인 데이터 포맷
{
    "_id" : ObjectId("5dd568ded61739fc4465af6f"),
    "time_period_start" : "1574267100000",
    "time_period_end" : "1574267159999",
    "price_open" : "8122.97000000",
    "price_high" : "8122.97000000",
    "price_low" : "8122.94000000",
    "price_close" : "8122.94000000",
    "volume_traded" : 3
}
### 악질적인 데이터 단순쿼리
db.getCollection('BTCUSD_1MIN').find({time_period_start: {$gt: new Date('2019-11-20T16:00:00.000Z').getTime().toString()}})

### 악질적인 데이터 검색 후 숫자 확인
db.getCollection('BTCUSD_1MIN').find({time_period_start: {$gt: new Date('2019-11-20T16:00:00.000Z').getTime().toString()}}).forEach(function(item){
    print(new Date(Number(item.time_period_start)))
})

이것도 먹힘
db.getCollection('BTCUSD_1MIN').find({time_period_start: {$gt: new Date('2019-11-20T16:00:00.000Z').getTime().toString()}}).forEach((item) => {
    print(new Date(Number(item.time_period_start)))
})


