```
 API Gateway

Method

POST : 데이터를 전송해주는 method

PUT : 

GET : 데이터를 수집하는 method

DELETE : 데이터를 삭제하는 method

DescribeStream : datastream의 정보를 조회하고 가져오는 권한 (kinesis)






API Gateway 권한


PutRecord : PutRecord는 하나의 Shard에 전송

PutRecords : Records는 모든 Shard에 전송


Mapping Templates
Aws “VTL” 사용
http 헤더 : Content-Type : 'application/x-amz-json1.1'

$input.params(‘  ’) : resource를 만들때 경로를 {data}로 적으면  아래처럼 된다
$input.path(‘  ‘) : data의 경로.. 를 적어놓고 호출합니다.

Requests : 사용자가 값은 주는 것을 받을떄
Response : 반환되는 값

# params
- singer는 {data} resource안에 있는 data

{
  "singer": $input.params($.data)
}

- 출력값
{
    "singer": {
        "korea": {
            "name": “jin”,
            "gender": "man"
        },
        "japen": {
            "name": “lee”,
            "gender": "girl"
        }
    }
}


# path

{
  "singer": $input.path($.singer)
  "singer-1-name": $input.path($.singer.korea.name)
}

- 출력값
{
  "singer": korea, japen
  "singer-1-name": “jin”




PutRecord

PutRecord-Requests
{
  "StreamName": "$input.params('stream')",
  "Data": "$util.base64Encode($input.body)",
  "PartitionKey": "$context.requestId"
}



 PutRecord-Requests  파티션 키 직접 설정 코드

{
  "StreamName": "$input.params('stream')",
  "Data": "$util.base64Encode($input.body)",
  "PartitionKey": "$input.path($.PartitionKey)"
}




CMD API Gatewate -> Kinesis(datastream) 데이터 전송 Code

http POST {api배포 url}/{datastream 이름}/record Data='전송할 데이터'
PartionKey=보내고 싶은 파티션 키






UpdateShardCount

UpdateShardCount-Requests 
- Kinesis DataStream Shard 수 (추가/삭제)


{
  "StreamName": "데이터스트림 이름",
  "TargetShardCount": $input.params('Resource 이름’'),
  "ScalingType": "UNIFORM_SCALING"
}



- Kinesis DataStream Shard 수 찾기
#set($count = $input.path('$.StreamDescriptionSummary.OpenShardCount'))
{
	"count" : $count
}


Kinesis DataStream -> Firehose

Kinesis DataStream (Glue Talbe)으로 데이터 전송해주기 위하여
Glue Table에 알맞은 값을 작성하여 -d ''에 넣어줍니다.

curl -X POST -H "Content-Type: application/json" -d '{ "변경": "넣고 싶은 데이터", "변경": "넣고 싶은 데이터" }' {api_gate deploy url}



```
