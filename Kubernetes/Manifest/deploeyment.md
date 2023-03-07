```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: (deployment 이름)
  namespace: (네임스페이스 이름)
spec:
  selector:
    matchLabels:
      type: (이름)
  replicas: (pod 갯수)
  template:
    metadata:
      labels:
        type: (이름)
    spec:
      containers:
      - name: (cluster 이름)
        image: (Ecr 이미지 URL)
        ports:
        - containerPort: (컨테이너 포트)

```
