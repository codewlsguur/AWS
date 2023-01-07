# Docker 명령어
```
usermod -aG docker ec2-user
systemctl enable --now docker
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
docker build -t (컨테이너 이름 or 파일 이름) .
docker run -d -p8080:8080 (파일 이름)
```
