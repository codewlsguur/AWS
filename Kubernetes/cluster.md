# eks 다운로드
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

# cluster.yaml
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: (클러스터 이름)
  region: ap-northeast-2
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
    private:
      ap-northeast-2a-priv: { id: (서브넷 아이디) }
      ap-northeast-2b-priv: { id: (서브넷 아이디) }
      ap-northeast-2c-priv: { id: (서브넷 아이디) }
managedNodeGroups:
  - name: skills-app
    instanceName: skills-app
    labels: { skills/dedicated: app }
    tags: { skills/dedicated: app }
    instanceType: c5.large
    minSize: 2
    maxSize: 20
    desiredCapacity: 2
    privateNetworking: true
    subnets:
     - ap-northeast-2a-priv
     - ap-northeast-2b-priv
     - ap-northeast-2c-priv
    iam:
      withAddonPolicies:
        imageBuilder: true
        autoScaler: true
        awsLoadBalancerController: true
        cloudWatch: true
  - name: skills-addon
    instanceName: skills-addon
    labels: { skills/dedicated: addon }
    tags: { skills/dedicated: addon }
    instanceType: c5.large
    minSize: 2
    maxSize: 20
    desiredCapacity: 2
    privateNetworking: true
    subnets:
     - ap-northeast-2a-priv
     - ap-northeast-2b-priv
     - ap-northeast-2c-priv
    iam:
      withAddonPolicies:
        imageBuilder: true
        autoScaler: true
        awsLoadBalancerController: true
        cloudWatch: true
```

# cluster 명령어
```
eksctl create cluster -f cluster.yaml
```
# cluster 삭제 명령어
```
eksctl delete cluster -f cluster.yaml 
```
