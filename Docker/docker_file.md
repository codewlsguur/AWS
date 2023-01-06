# Dockerfile
```
FROM ubuntu:latest
COPY ./match .
RUN apt update -y && apt install curl -y
RUN adduser match
USER match
EXPOSE 8080
CMD ["./match"]
```
# Docker 명령어
```
docker build -t 이름 .
docker run -d -p8080:8080 이름
```