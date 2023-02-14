# ./k8s/service.yml
```
apiVersion: v1
kind: Service

metadata:
  name: (이름 1)-service
  namespace: (네임스페이스 이름)
spec:
  selector:
    skills/version: v1
    type: (이름 1)
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
  type: NodePort
---
apiVersion: v1
kind: Service

metadata:
  name: (이름 2)-service
  namespace: (네임스페이스 이름)
spec:
  selector:
    skills/version: v1
    type: (이름 2)
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
  type: NodePort
```
