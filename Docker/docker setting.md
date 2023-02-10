# FROM : 사용할 언어:(버전)
# RUN : 실행할 명령
# COPY : 복사
# EXPOSE : 포트번호
# WORKDIR : 파일 생성후 파일안에서 작업 수행
# USER : 사용자 설정
# CMD : ["실행할 파일 이름"]
#
#

# 파일 권한 주기 (cmd)
```
chmod 777 ./(파일이름)
```
# 파일 권한 주기 (Dockerfile)
```
RUN chmod 777 ./(파일이름)
```
# 사용자 생성 명령어
```
RUN adduser (이름)
```
# 사용자 사용 명령어
```
USER (이름)
```
