# PassWord to EC2
```
sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
sudo echo -e "(비밀번호)\n(비밀번호)" | sudo passwd ec2-user
systemctl restart sshd
```
