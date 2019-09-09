Kubernetes - AWS
================

환경별로 설치 및 사용법이 너무 달라서 별도로 정리

클러스터 생성에서 인증까지

## 사전설치 항목
### aws-cli
필수설치
### kubectl
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/install-kubectl.html
### aws-iam-authenticator
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/install-aws-iam-authenticator.html
### eksctl
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html
선택아님. 필수설치

## AWS 설정
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/network_reqs.html
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/create-public-private-vpc.html

## Create Cluster

### eksctl
https://eksctl.io/usage/schema/

대부분의 설정을 eksctl에 위임한 형태\
잘 모르면 기본셋팅으로 이렇게 사용하는게 좋다\
기존 vpc에 넣으려고 하면 nat게이트웨이 등 세부적인 설정을 해 줘야하는데\
이 과정에서 오류가 발생해서 nodegroup과 master통신이 안되서 노드 인식을 못하는 문제가 발생하기도 한다.
```yaml
# basic-cluster.yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: basic-cluster
  region: ap-northeast-2

vpc:
  cidr: "172.11.0.0/16"

nodeGroups:
  - name: ng-1-private
    instanceType: t3.medium
    desiredCapacity: 2
    privateNetworking: true
    ssh:
      allow: true # will use ~/.ssh/id_rsa.pub as the default ssh key
  - name: ng-2-public
    instanceType: t3.medium
    desiredCapacity: 2
    ssh:
      publicKeyPath: ~/.ssh/ec2_id_rsa.pub
```

커스텀 해서 쓰려면\
이런식으로 하면 되는데\
네트워크 설정을 잘못 해 놓는 경우 오류발생
```yaml
# cluster-with-vpn.yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: dev-tmp1-eks
  region: ap-northeast-2

vpc:
  subnets:
    private:
      eu-north-1a: { id: subnet-0ff156e0c4a6d300c }
      eu-north-1b: { id: subnet-0549cdab573695c03 }
      eu-north-1c: { id: subnet-0426fb4a607393184 }

nodeGroups:
  - name: ng-1-workers
    labels: { role: workers }
    instanceType: m5.xlarge
    desiredCapacity: 10
    privateNetworking: true
  - name: ng-2-builders
    labels: { role: builders }
    instanceType: m5.2xlarge
    desiredCapacity: 2
    privateNetworking: true
    iam:
      withAddonPolicies:
        imageBuilder: true
```

설정파일 이용해서 실행
`eksctl create cluster -f <cluster-filename.yaml>`

설정파일 이용해서 삭제
`eksctl delete cluster -f <cluster-filename.yaml>`

클러스터 이름으로 삭제
`eksctl delete cluster --name=dev-tmp2-eks`

## 기 생성된 클러스테의 노드 관리
https://eksctl.io/usage/managing-nodegroups/

시큐리티 그룹을 다 넣으면 오류가남. 웹콘솔에서는 잘 되는데
웹콘솔에서 클러스터 생성하고 여기서는 노드그룹만 생성하는 것도

```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: dev-cluster
  region: eu-north-1

nodeGroups:
  - name: ng-1-workers
    labels: { role: workers }
    instanceType: m5.xlarge
    desiredCapacity: 10
    privateNetworking: true
  - name: ng-2-builders
    labels: { role: builders }
    instanceType: m5.2xlarge
    desiredCapacity: 2
    privateNetworking: true
```

```text
eksctl create nodegroup --config-file=<path> \
--include=<ng-include-1,ng-include-2> \
--exclude=<ng-exclude-1,ng-exclude-2>
```

노드그룹 삭제
`eksctl delete nodegroup --config-file=<dev-cluster.yaml> --exclude=<nodename>`
`eksctl delete nodegroup --cluster=<clustername> --name=<nodegroup>`

노드그룹 드레인??
`eksctl drain nodegroup --cluster=<clustername> --name=<ndoegroupname> --undo`

### web console
대강 이름 정하고 시큐리티그룹 넣어주고
iam을 직접 생성해야한다.
대강 eks 관련됨거 검색해서 다 넣어줬는데 세부적인건 확인필요
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/security-iam.html

VPC, Security Group 선택

노드그룹 추가
https://docs.aws.amazon.com/eks/latest/userguide/launch-workers.html
https://eksctl.io/usage/managing-nodegroups/

웹콘솔은 쓰지말자. 제대로 되지도 않음

## 노드 생성 확인
eksctl get nodegroup --cluster <cluster-name>

## 인증
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/managing-auth.html
aws-iam-authenticator 설치 후

aws eks --region <region-name> update-kubeconfig --name <cluster-name>

내부 API 접근 허용.. 안해놓으면 노드인식안될수있음
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/cluster-endpoint.html
aws eks --region region update-cluster-config --name dev --resources-vpc-config endpointPublicAccess=false,endpointPrivateAccess=true
