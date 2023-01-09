# public
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: (이름)-ingress
  namespace: skills
  annotations:
    alb.ingress.kubernetes.io/load-balancer-name: stress
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/subnets: skills-public-a, skills-public-b, skills-public-c
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
  namespace: skills
  annotations:
    alb.ingress.kubernetes.io/load-balancer-name: stress
    alb.ingress.kubernetes.io/scheme: internal
    alb.ingress.kubernetes.io/subnets: skills-private-a, skills-private-b, skills-private-c
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