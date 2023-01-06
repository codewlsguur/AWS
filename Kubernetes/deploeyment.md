```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stress-deployment
  namespace: (이름)
spec:
  selector:
    matchLabels:
      type: stress
  replicas: 2
  template:
    metadata:
      labels:
        skills/version: v1
        type: stress
    spec:
      containers:
      - name: stress-container
        image: (이미지 URL)
        ports:
        - containerPort: 8080
        resources:
          limits:
            cpu: 500m
          requests:
            cpu: 200m
```