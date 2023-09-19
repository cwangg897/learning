![image](https://github.com/cwangg897/learning/assets/79621675/cf1bfb53-66ac-4918-8d12-39d06b729a34)#### 헷갈리는거
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
kubectl rollout undo deploy http-go (이렇게하면 버전하나가 내려간다)
특정 버전으로 돌아가는경우
kubectl rollout undo deploy http-go --to-revision = 1
히스토리 revision번호임
```



#### 연습문제
![image](https://github.com/cwangg897/learning/assets/79621675/e09b7fd3-9179-45d3-a182-708447b2cde8)


![image](https://github.com/cwangg897/learning/assets/79621675/cde37be2-454c-404a-81a6-b57d71f1e6e3)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: alpine-test
  labels:
    app: alpine-test
spec:

  strategy:
    rollingUpdate:
      maxSurge : 50%
      maxUnavailable: 50%
    type : RollingUpdate
  replicas: 10
  selector:
    matchLabels:
      app: alpine-test
  template:
    metadata:
      labels:
        app: alpine-test
    spec:
      containers:
      - name: alpine
        image: alpine:3.4
        ports:
        - containerPort: 80
kubectl crate deploy alpine-test --record=true
kubectl rollout history deploy alpine-test (기록보기)
kubectl set image deploy alpine-test alpine-test=alpine:3.5 --record=true, kubectl edit deploy alpine-test --record=true
kubectl rollout undo deploy alpine-test --to-revision = 1
```

