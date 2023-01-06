# PassWord to EC2
```
sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config
sudo echo -e "Leewlsgur0525@#\nLeewlsgur0525@#" | sudo passwd ec2-user
systemctl restart sshd
```
