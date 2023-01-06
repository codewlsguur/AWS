```
apiVersion: v1
kind: Service

metadata:
  name: (이름)-service
  namespace: skills
spec:
  selector:
    skills/version: v1
    type: (이름)
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
  type: NodePort
```