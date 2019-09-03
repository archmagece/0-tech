Kubernetes
==========

## Kube 설치 환경별 활용법
AWS와 GCP, 로컬에서 설치가 조금씩 다를 수 있음

### GCP
그냥 콘솔이나 명령어로 실행시키면 바로 사용가능

### AWS
역시 AWS는 좆같은게 웹콘솔에서 해서는 제대로 되지 않는다
eksctl을 가지고 컨트롤해야함
API를 통해서 처리해야하는 것 같다.
웹콘솔이 없으면 씨발 오픈을 하지 말라고 이거 이틀 날려먹었네

kubectl describe pod/--name--- 을 이용해서 에러를 확인하고 구글 검색해서 겨우 처리

#### eksctl
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html

#### create cluster
```
eksctl create cluster \
--name dev-tmp1-eks \
--version 1.13 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto \
--full-ecr-access \
--vpc-private-subnets subnet-00000000,subnet-000000
--vpc-public-subnets subnet-0000000,subnet-000000
```

```
eksctl delete cluster dev-tmp1-eks
```

#### kubectl
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/install-kubectl.html

aws eks --region ap-northeast-2 update-kubeconfig --name dev-tmp-eks

#### 셋팅이 잘 됐는지 테스트
https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/

kubectl apply -f https://k8s.io/examples/application/deployment.yaml
kubectl get po,svc,rc,deploy
kubectl describe deployment nginx-deployment

### minik8s

이것도 뭔가 좀 애매한 면이 있다.
바로 사용이 안된다. 돈걱정없으면 그리고 꼭 로컬에서 뭘 해야겠다는게 아니면 GCP에서 연습하는게 편하지 않을까


## 설정 관리

## 컨테이너 설정파일 관리 config map

https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/

## 환경변수 env variable

https://kubernetes.io/ko/docs/tasks/inject-data-application/define-environment-variable-container