```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: (디플로이멘트 이름)
  namespace: (네임스페이스 이름)
spec:
  selector:
    matchLabels:
      type: (이름)
  replicas: 2
  template:
    metadata:
      labels:
        skills/version: v1
        type: (이름)
    spec:
      nodeSelector:
        (??????)
      containers:
      - name: (이름)-container
        image: (ecr 이미지 URL)
        ports:
        - containerPort: 8080
        resources:
          limits:
            cpu: 500m
          requests:
            cpu: 200m
```
