# Jenkins 설치
## 인스턴스를 최신버전으로 업데이트합니다.
```
sudo yum update –y
```
## Jenkins 저장소를 추가합니다.
```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
## 설치할 수 있도록 키파일을 가져옵니다.
```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
```
sudo yum upgrade -y
```
## 자바를 설치합니다.
```
sudo amazon-linux-extras install java-openjdk11 -y
```
## Jenkins를 설치합니다.
```
sudo yum install jenkins -y
```
## Jenkins를 활성화 합니다.
```
sudo systemctl enable jenkins
```
## Jenkins를 시작합니다.
```
sudo systemctl start jenkins
```
## Jenkins에 접속하기 위해 <인스턴스의 퍼블릭IP>:8080 으로 접속합니다.

## Jenkins암호를 확인합니다.
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Jenkins에 로그인한 후 Jenkins관리 > 플러그인 관리 > Available plugins 로 가서 AWS CodePipeline을 설치합니다.
