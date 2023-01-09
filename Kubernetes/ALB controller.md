# IAM 설치 (1회 사용)
```
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.3.1/docs/install/iam_policy.json
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
```

# eks
```
eksctl utils associate-iam-oidc-provider \
    --region ap-northeast-2 \
    --cluster worldskills-cloud-cluster \
    --approve
```

```
kubectl apply -k github.com/aws/eks-charts/stable/aws-load-balancer-controller/crds?ref=master
```

```
eksctl create iamserviceaccount \
    --cluster=(이름) \
    --namespace=kube-system \
    --name=aws-load-balancer-controller \
    --attach-policy-arn=arn:aws:iam::(AWS 사용자 아이디):policy/AWSLoadBalancerControllerIAMPolicy \
    --override-existing-serviceaccounts \
    --approve
```

```
wget https://github.com/jetstack/cert-manager/releases/download/v1.5.4/cert-manager.yaml
```
```
kubectl apply -f cert-manager.yaml --validate=false
```
```
curl -Lo ALB.yaml https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.4/v2_4_4_full.yaml
```

```
sed -i.bak -e '480,488d' ./ALB.yaml
```
```
sed -i.bak -e 's|(cluster 이름)|(cluster 이름)|' ./ALB.yaml
```

```
kubectl apply -f ALB.yaml
kubectl apply -f https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.4/v2_4_4_ingclass.yaml
```
```
kubectl get sa aws-load-balancer-controller -n kube-system -o yaml
```
