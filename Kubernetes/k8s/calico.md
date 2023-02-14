# install calico
```
wget https://raw.githubusercontent.com/aws/amazon-vpc-cni-k8s/master/config/master/calico-operator.yaml
wget https://raw.githubusercontent.com/aws/amazon-vpc-cni-k8s/master/config/master/calico-crs.yaml
```
```
kubectl apply -f calico-operator.yaml
kubectl apply -f calico-crs.yaml
```
```
kubectl get daemonset calico-node --namespace calico-system
```
