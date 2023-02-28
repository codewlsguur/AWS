# scripts/after.sh
```
pip3 install flask [설치모듈]
```

# scripts/stop.sh (파이썬 정지)
```
pkill -9 python
```

# scripts/start.sh
```
python3 /home/ec2-user/app.py > /dev/null 2> /dev/null < /dev/null &
```
