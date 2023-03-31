# API GATEWAY KINESIS
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

# ECS
```
ECS - Fargate (WebProvisioning)

Ec2 instance를 먼저 Public으로 만들어 접속한후, Dockerfile을 작성하여 줍니다.

ECS를 만들기 위해선 ECR(Dockerfile) 이 필요하기 때문에 ECR에 Dockerfile을
업로드 해줍니다.


Docker 설치 명령어

sudo yum install docker -y
sudo usermod -aG docker ec2-user
sudo systemctl enable --now docker
sudo su ec2-user



Dockerfile을 업로드 하기 위해서는 

docker build -t (docker image 이름) .
docker run -d -p(포트번호):(포트번호)  (docker image 이름)


ECR에서 업로드를 확인하고, ELB를 만들어줍니다.

ALB 사용 - 대상그룹을 이용하여 ALB를 만들고 리스너를 삭제합니다.
NLB 사용 - 대상그룹(alb) 선택,  ALB를 만들고 NLB를 만들고 리스너를 삭제합니다.


ECS로 접속하여 “작업정의(Task Definitions)”를 만들어줍니다.
작업정의에서 Fargate를 선택해줍니다.


작업정의에서 “컨테이너 추가” 컨테이너를 작성해줍니다.
컨테이너 포트는 app의 포트를 작성해줍니다.
용량은 기본 512를 추천하고, 완료를 누릅니다.

ECS에서 Fargate를 골라 Cluster를 만들어주고,
service를 만들어줍니다.

service에서 ELB를 연결할떄 listener 포트는 “80”으로 해줘야한다 (필수)

ECS - EC2/Instance (CICD)


Ec2 instance를 먼저 Public으로 만들어 접속한후, Dockerfile을 작성하여 줍니다.

ECS를 만들기 위해선 ECR(Dockerfile) 이 필요하기 때문에 ECR에 Dockerfile을
업로드 해줍니다.


Docker 설치 명령어

sudo yum install docker -y
sudo usermod -aG docker ec2-user
sudo systemctl enable --now docker
sudo su ec2-user



Dockerfile을 업로드 하기 위해서는 

docker build -t (docker image 이름) .
docker run -d -p(포트번호):(포트번호)  (docker image 이름)


ECR에서 업로드를 확인하고, ELB를 만들어줍니다.

ALB 사용 - 대상그룹을 이용하여 ALB를 만들고 리스너를 삭제합니다.
NLB 사용 - 대상그룹(alb) 선택,  ALB를 만들고 NLB를 만들고 리스너를 삭제합니다.


ECS로 접속하여 “작업정의(Task Definitions)”를 만들어줍니다.
작업정의에서 EC2/Instance를 선택해줍니다.


작업정의에서 “컨테이너 추가” 컨테이너를 작성해줍니다.
컨테이너 포트는 app의 포트를 작성하고 Host는 0으로 작성해줍니다.
용량은 기본 512를 추천하고, 완료를 누릅니다.

ECS에서 EC2를 골라 Cluster를 만들어주고,
service를 만들어줍니다.

service에서 ELB를 연결할떄 listener 포트는 “80”으로 해줘야한다 (필수)

```
# DOCKER
```


Install Docekr & Build/Run


Docker Install Code

sudo yum install docker -y
sudo usermod -aG docker ec2-user
sudo systemctl enable --now docker
sudo su ec2-user



Docker Build Code

sudo docker build -t (저장 하고 싶은 파일 이름) .


Docekr Run Code

sudo docker run -d -p(포트번호):(포트번호) (파일 이름)



Local host
curl localhost:(숫자(상관없음))/health

Delete Docker Build
docker kill (docker container id)

Delete Docker Run
docker rmi -f (docker images id)


Docker Image 확인
docker images
Dockerfile


FROM : 사용할 언어:(버전)
RUN : 실행할 명령
COPY : ./ 복사할 파일 이름 .
EXPOSE : 포트번호
WORKDIR : 파일 생성후 파일안에서 작업 수행
USER : 사용자 설정
CMD : ["실행할 파일 이름"]



파일 권한 주는 Code (CMD)
chmod 777 ./(파일이름)

파일 권한 주는 Code (Dockerfile)
RUM chmod 777 ./(파일이름)

사용자 생성 명령어
RUN adduser (이름)

사용자 사용 명령어
USER (이름)


python : CMD ["python", “./(파일 이름)”]
그 외 : CMD ["./(파일 이름)"]


```

# starttemplate
```
Install


AWS CLI
EKS CTL


KUBE CTL

최신버전 curl..을 설치하고, chmod 권한을 준후
mv ./kubectl /usr/local/bin
코드를 넣어줍니다.

StartTemplate

Port번호를 변경해주는 코드

echo 'Port (포트 번호)' >> /etc/ssh/sshd_config
systemctl restart sshd




ec2-instance 접속 비밀번호를 설정해주는 코드

sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
sudo echo -e "(비밀번호)\n(비밀번호)" | sudo passwd ec2-user
systemctl restart sshd




```
