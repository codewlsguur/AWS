# buildspec.yml
```
version: 0.2

phases:
  pre_build:
    commands:
      - <commands>
  build:
    commands:
      - <commands>
  post_build:
    commands:
      - <commands>
artifacts:
  files:
    - 'appspec.yml'
    - 'scipts/before.sh'
    - 'scipts/after.sh'
    - 'scipts/start.sh'
    - 'scipts/stop.sh'
```

```
  install:
    runtime-versions:
      <language>: <version>  #EX) python: 3.8
```