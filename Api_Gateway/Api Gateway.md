# 필요에 맞게 사용 
### PutRecord는 하나의 Shard에 전송 Records는 모든 Shard에 전송
```
PutRecrod
```
```
PutRecrods
```

# Kinesis DataStream (Glue Talbe) 으로 데이터 전송
### Glue Table에 알맞은 값을 작성하여 -d ''에 넣어줍니다
```
curl -X POST -H "Content-Type: application/json" -d '{ "변경": "넣고 싶은 데이터", "변경": "넣고 싶은 데이터" }' {api_gate deploy url}
```
