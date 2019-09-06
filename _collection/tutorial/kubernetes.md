Kubernetes
==========

## Kube 설치 환경별 활용법
AWS와 GCP, 로컬에서 설치가 조금씩 다를 수 있음

요즘은 helm 설치가 필수적이라 이 부분도 포함  

### onPremise
microk8s
minikube
k3s

### on GCP
그냥 콘솔이나 명령어로 실행시키면 바로 사용가능

### on Azure
어떻게 하지

### on AWS
역시 AWS는 좆같은게 웹콘솔에서 해서는 제대로 되지 않는다 \
eksctl을 가지고 컨트롤해야 하고 신경 써 줘야 하는게 많다 \
kube클러스터를 위한 인프라를 만든게 아니고 cloud formation을 통해 노드를 컨트롤 하는 방식인 것 같다. 이로 인해서 발생하는 오류가 많은 것 같다 \
웹콘솔이 없으면 씨발 오픈을 하지 말라고 이거 이틀 날려먹었네(그리고 앞으로 이틀씩 몇번을 더 날려먹겠지) \

웹콘솔에서 클러스터를 생성하고 aws-iam-authenticator 설치해서 인증처리도 했는데 \
kubectl apply -f app-deployment.yaml을 해도 계속 PENDING이라서 \
kubectl describe pod/--name--- 을 이용해서 에러를 확인 \
no nodes 어쩌고 메시지가 떴던 것 같다. 노드가 없다는게 이해가 안갔다 \
당연히 자동으로 들어가는 줄 알았지.. 클러스터 서버 갯수 선택하는게 없어서 이상하긴 했지만... \
노드가 생성이 안 돼 있었다. eksctl을 이용해서 노드그룹을 추가 해 줘야한다.

## 필수 설치 및 사용
### kubectl
https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/install-kubectl.html

각 환경별 kubectl 로그인 방법대로 로그인
 
### 셋팅이 잘 됐는지 테스트
https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/

https://k8s.io/examples/application/deployment.yaml
```
apiVersion: apps/v1 # apps/v1beta2를 사용하는 1.9.0보다 더 이전의 버전용
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # 템플릿에 매칭되는 파드 2개를 구동하는 디플로이먼트임
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

```
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
kubectl get po,svc,rc,deploy
kubectl describe deployment nginx-deployment
```

## 설정 관리

### 컨테이너 설정파일 관리 config map

https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/

### 환경변수 env variable

https://kubernetes.io/ko/docs/tasks/inject-data-application/define-environment-variable-container


## Namespace
https://kubernetes.io/ko/docs/concepts/overview/working-with-objects/namespaces/

```
kubectl get namespace
kubectl craete ns <name>

kubectl api-resources --namespaces=true
kubectl api-resources --namespaces=false
```



## 배포 후 확인
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/



