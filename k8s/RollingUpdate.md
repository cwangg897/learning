#### 헷갈리는거
중요한거는 파일이름이 아니라 metadata이름을 가지고 같은건지 알아보는것이다

#### v1 실습
```yaml
apiVersion: apps/v1

kind : Deployment

metadata:
  name : http-go
  labels:
    app: http-go

spec:
  replicas: 5
  selector:
    matchLabels:
      app: http-go
  template:
    metadata:
      name : http-go
      labels:
        app: http-go
    spec:
      containers:
        image : http-go
        name : gasbugs/http-go:v1
        ports:
          containerPort: 8080


kubectl create -f http-go-deploy-v1.yaml --record=true 이래야지 꼭 히스토리에 남아서 백업이 가능하다
업데이트하는방법
kubectl set image deploy http-go http-go=gasbugs/http-go:v2  
다운타임이 발생하는것은 중지중이면서 새로온것은 pending이기때문에
그런데 하나에 파드에 다운타임이 발생하는거지 전체적인 서비스는 다운타임이 발생하는것은 아니다
업데이트할떄마다 replicaSet이 새로생기고 이전 replicaSet은 replicas를 0으로 만든것이다
set image = yaml파일을 바꾸는거랑 같다
kubectl edit deploy http-go --record=true
kubectl rollout history deploy http-go (이렇게하면 버전하나가 내려간다)
특정 버전으로 돌아가는경우
kubectl rollout undo deploy http-go --to-revision = 1
히스토리 revision번호임
```
