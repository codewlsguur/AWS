# cluster 명령어
```
eksctl create cluster -f cluster.yml
```
# cluster 삭제 명령어
```
eksctl delete cluster -f cluster.yml 
```
# cluster.yaml
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: (클러스터 이름)
  region: ( 리전 )
  version: "1.22"
cloudWatch:
  clusterLogging:
    enableTypes:
    - "api"
    - "audit"
    - "authenticator"
    - "controllerManager"
    - "scheduler"

iam:
  withOIDC: true
vpc:
  id:
  subnets:
    public:
      ap-northeast-2a-pub: { id: (서브넷 아이디) }
      ap-northeast-2b-pub: { id: (서브넷 아이디) }
      ap-northeast-2c-pub: { id: (서브넷 아이디) }
      ap-northeast-2d-pub: { id: (서브넷 아이디) }
    private:
      ap-northeast-2a-priv: { id: (서브넷 아이디) }
      ap-northeast-2b-priv: { id: (서브넷 아이디) }
      ap-northeast-2c-priv: { id: (서브넷 아이디) }
      ap-northeast-2d-priv: { id: (서브넷 아이디) }
```
# 노드그룹 추가
```
managedNodeGroups:
  - name: ( 노드그룹 이름 )
    instanceName: ( 인스턴스 이름 )
    instanceType: ( 인스턴스 type )
    minSize: 2
    maxSize: 20
    desiredCapacity: 2
    privateNetworking: true
    subnets:
     - ap-northeast-2a-priv
     - ap-northeast-2b-priv
     - ap-northeast-2c-priv
     - ap-northeast-2d-priv
    iam:
      withAddonPolicies:
        imageBuilder: true
        autoScaler: true
        awsLoadBalancerController: true
        cloudWatch: true
```
# Fargate
```
fargateProfiles:
  - name: <>
    selectors:
      - namespace: <>
  - name: <>
    selectors:
      - namespace: <>
```
# Fargate 라벨 추가
```
selectors:
    labels:
        env: <>
        checks: <>
```

