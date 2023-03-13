# Docker 명령어
```
sudo usermod -aG docker ec2-user
sudo systemctl enable --now docker
sudo su ec2-user
```

# vi Dockerfile
```
FROM (사용언어):latest
COPY ./ (파일 이름) .
RUN apt update -y && apt install curl -y
RUN adduser (파일 이름)
USER (파일 이름)
EXPOSE 8080
CMD ["./(파일 이름)"]
```
# Docker build 명령어
```
sudo docker build -t (저장 하고 싶은 파일 이름) .
sudo docker run -d -p(숫자(상관없음)):(포트번호) (파일 이름)
```
# local host
```
curl localhost:(숫자(상관없음))/health
```

# Docker Build 지우는법
```
docker kill (docker container id)
```
# Docker Run 지우는법
```
docker rmi -f (docker images id)
```
