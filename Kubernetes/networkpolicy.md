
# Network Policy (calico)
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: (이름)-network
  namespace: (네임스페이스 이름)
spec:
  podSelector:
    matchLabels:
      type: (이름)
  policyTypes:
    - Egress
  egress:
    - to:
        - ipBlock:
            cidr: 0.0.0.0/0
      ports:
        - port: 443
        - port: 80
        - port: 53
          protocol: TCP
        - port: 53
          protocol: UDP
```

# networkpolicy 실행 명령어
```
kubectl apply -f (파일위치)/networkpolicy.yaml
```
