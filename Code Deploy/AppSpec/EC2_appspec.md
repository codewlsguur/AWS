# appsepc.yml
```
version: 0.0
os: linux
files:
  - source: /
    destination: /home/ec2-user
hooks:
  AfterInstall:
    - location: <sh_location>
      timeout: 180
      runas: root
  ApplicationStart:
    - location: <sh_location>
      timeout: 180
      runas: root
  ApplicationStop:
    - location: <sh_location>
      timeout: 180
      runas: root
```