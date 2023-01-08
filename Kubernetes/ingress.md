# public
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: (이름)-ingress
  namespace: (네임스페이스 이름)
  annotations:
    alb.ingress.kubernetes.io/load-balancer-name: (이름)
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/subnets: (서브넷 이름), (서브넷 이름), (서브넷 이름)
    alb.ingress.kubernetes.io/target-type: instance
    alb.ingress.kubernetes.io/healthcheck-path: /health
    alb.ingress.kubernetes.io/target-node-labels: skills/dedicated=app
    alb.ingress.kubernetes.io/actions.response-403: >
      {"type":"fixed-response","fixedResponseConfig":{"contentType":"text/plain","statusCode":"403","messageBody":"403 error text"}}
spec:
  ingressClassName: alb
  rules:
  - http:
      paths:
      - path: "/v1/"
        pathType: Prefix
        backend:
          service:
            name: (이름)-service
            port:
              number: 80
      - path: /
        pathType: Prefix
        backend:
          service:
            name: response-403
            port:
              name: use-annotation
```

# private
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: (이름)-ingress
  namespace: (네임스페이스 이름)
  annotations:
    alb.ingress.kubernetes.io/load-balancer-name: (이름)
    alb.ingress.kubernetes.io/scheme: internal
    alb.ingress.kubernetes.io/subnets: (서브넷 이름), (서브넷 이름), (서브넷 이름)
    alb.ingress.kubernetes.io/target-type: instance
    alb.ingress.kubernetes.io/healthcheck-path: /health
    alb.ingress.kubernetes.io/target-node-labels: skills/dedicated=app
    alb.ingress.kubernetes.io/actions.response-403: >
      {"type":"fixed-response","fixedResponseConfig":{"contentType":"text/plain","statusCode":"403","messageBody":"403 error text"}}
spec:
  ingressClassName: alb
  rules:
  - http:
      paths:
      - path: "/v1/"
        pathType: Prefix
        backend:
          service:
            name: (이름)-service
            port:
              number: 80
      - path: /
        pathType: Prefix
        backend:
          service:
            name: response-403
            port:
              name: use-annotation
```

# ingress 실행 명령어
```
kubectl apply -f (파일위치)/ingress.yaml
```
# ingress 삭제 명령어
```
kubectl delete -f (파일위치)/ingress.yaml
```
