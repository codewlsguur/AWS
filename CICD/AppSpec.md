# appspec.yml
```
version: 0.0
os: linux
files:
  - source: /
    destination: /home/ec2-user
hooks:
  BeforeInstall:
    - location: scripts/before.sh
      timeout: 180
      runas: root

  AfterInstall:
    - location: scripts/after.sh
      timeout: 180
      runas: root

  ApplicationStart:
    - location: scripts/start.sh
      timeout: 180
      runas: root

  ApplicationStop:
    - location: scripts/stop.sh
      timeout: 180
      runas: root

```

```
  install:
    runtime-versions:
      <language>: <version>  #EX) python: 3.8
```