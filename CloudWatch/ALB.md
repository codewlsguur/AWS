# ARN "alb/..." 으로 CloudWatch에 검색


```
서버의 5XX 응답값
AppELB별 지표 -> HTTPCode_Target_5xx_Count
```


```
LB의 5XX 응답값에 대한 메트릭
AppELB별 지표 -> HTTPCode_ELB_5xx_Count
```


```
LB로 유입 되는 HTTP 요청 개수에 대한 메트릭 포함
AppELB별 지표 -> RequestCount
```


```
LB로 들어오는 HTTP 요청의 평균 응답 시간 메트릭 포함
AppELB별 지표 -> TargetResponseTime
```