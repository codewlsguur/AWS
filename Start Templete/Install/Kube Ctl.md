# kubernetes 1.23
```
curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.23.7/2022-06-29/bin/linux/amd64/kubectl
```
# kubernetes 실행 권한
```
chmod +x ./kubectl
```
# kubernetes 관련 파일 생성
```
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
```
# kubernetes 파일 이동
```
mv ./kubectl /usr/local/bin
```