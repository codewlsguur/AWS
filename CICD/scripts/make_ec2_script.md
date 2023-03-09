# ec2_launch.sh
```
aws ec2 run-instances \
    --image-id ami-0f6e451b865011317 \
    --instance-type t3.small \
    --count 1 \
    --subnet-id subnet-09fc1b6b64dc8258b \
    --user-data ./data.txt \
    --security-group-ids sg-00fe6476c6d6eff09 \
    --iam-instance-profile Name=PowerUser \
    --tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value=$1},{Key=wsi:deploy:group,Value=dev-api}]"
```

# data.txt
```
#!/bin/bash
[EC2 시작 템플릿 코드]
```

# Code
```
./ec2_launch.sh [만들 EC2 이름]
```