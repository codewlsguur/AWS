# Aws Logs 다운로드
```
sudo yum install -y awslogs
```

# log 정보 변경
```
sudo yum install -y awslogs
systemctl start awslogsd
systemctl enable awslogsd
cat<<EOF >>/etc/awslogs/awslogs.conf
[로그그룹 이름]
datetime_format = %b %d %H:%M:%S
file = 저장 파일 위치
log_stream_name = {instance_id}
initial_position = start_of_file
log_group_name = 로그그룹 이름
EOF

sudo systemctl restart awslogsd
sed -i "s/us-east-1/( 리전 이름 )/g" /etc/awslogs/awslogs.conf
```
