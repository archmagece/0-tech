Kubernetes Helm
====

## 구성요소
### HELM : Kubernetes Package Manager
https://github.com/helm/helm
redis, kafka, jenkins, flink 등 kubernetes cluster에서 설치해서 사용하는 툴을 미리 정의 해놓고 쉽게 사용할 수 있게 해 주는 툴

### Chart
https://github.com/helm/charts
HEML의 설계도?

### Chartmuseum
https://github.com/helm/chartmuseum
차트 저장소

### 차트 만들기
#### Create from Chart Skeleton
` helm create <My ChartName>`

```text
flink
├── Chart.yaml
├── charts
├── templates
│   ├── NOTES.txt
│   ├── _helpers.tpl
│   ├── deployment.yaml
│   ├── ingress.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml

3 directories, 8 files
```

#### Create from Existing Chart
` helm fetch stable/redis`

압축파일을 다운로드 하는데 압축을 풀어서 편집

`tar zxvf redis-*.tgz`

#### Install Chart
helm install ./redis
helm install stable/redis

#### Package Chart
helm package ./redis

챠트 배포
curl --data-binary "@redis-0.0.1.tgz" http://localhost:8080/api-charts
{"saved":true}

챠트 배포 확인
curl http://localhost:8080/api-charts

#### 챠트 리포지터리 등록
helm repo add --username <usernmae> --password <password> my-chartmuseum http://localhost:8080/api-charts


### Install on Kubernetes
https://docs.microsoft.com/ko-kr/azure/aks/kubernetes-helm
https://helm.sh/docs/