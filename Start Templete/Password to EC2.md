# PassWord to EC2
```
sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
sudo echo -e "(비밀번호)\n(비밀번호)" | sudo passwd ec2-user
systemctl restart sshd
```
```
nginx:latest
CMD-SHELL, curl -f http://localhost:80/health || exit 1

git add .
git branch -M (브런치 이름)
git commit -m "dd"
git push origin upstream
