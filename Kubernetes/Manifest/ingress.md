# public
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: (ingress 이름)
  namespace: (네임스페이스 이름)
  annotations:
    alb.ingress.kubernetes.io/load-balancer-name: ( ALB 이름 )
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/subnets: (서브넷 이름)
    alb.ingress.kubernetes.io/target-type: (instance or ip)
    alb.ingress.kubernetes.io/healthcheck-path: /health
 
spec:
  ingressClassName: alb
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: ( service 이름 )
            port:
              number: (port 번호)
```

# private
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: (ingress 이름)
  namespace: (네임스페이스 이름)
  annotations:
    alb.ingress.kubernetes.io/load-balancer-name: ( ALB 이름 )
    alb.ingress.kubernetes.io/scheme: internal
    alb.ingress.kubernetes.io/subnets: (서브넷 이름)
    alb.ingress.kubernetes.io/target-type: (instance or ip)
    alb.ingress.kubernetes.io/healthcheck-path: /health

spec:
  ingressClassName: alb
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: ( service 이름 )
            port:
              number: (port 번호)
```

# ingress 실행 명령어
```
kubectl apply -f (파일위치)/ingress.yaml
```
# ingress 삭제 명령어
```
kubectl delete -f (파일위치)/ingress.yaml
```
