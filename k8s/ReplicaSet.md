#### 중요
레플리카셋은 파드와 종류가 다르다 다른 종류다
그래서 같은이름이라도 `kubectl get pod hello, kubectl get rc hello` 이렇게 가능하다

#### 레플리카셋의 구버전은 레플리케이션 컨트롤러
```
- 포드가 항상 실행되도록 유지하는 쿠버네티스 리소스
- 노드가 클러스터에서 사라지는 경우 해당 포드를 감지하고 대체 포드 생성
- 실행 중인 포드의 목록을 지속적으로 모니터링으로 하고 '유형'의 실제 포드 수가 원하는 수와 항상 일치하는지 확인

레이블이 달라지면 다른 파드로봄 그래서 새로운 파드를 생성해버림
```


#### 레플리케이션 컨트롤러의 세 가지 요소
- 레플리케이션 컨트롤러가 관리하는 포드 범위를 결정하는 레이블 셀렉터
- 실행해야 하는 포드의 수를 결정하는 복제본 수
- 새로운 포드의 모양을 설명하는 포드 템플릿

  #### 레플리케이션컨트롤러의 장점
  - 포드가 없는 경우 새 포드를 항상 실행
  - 노드에 장애 발생 시 다른 노드에 복제본 생성
  - 수동, 자동으로 수평(scale-out) 스케일링
 

#### 실습
주의사항은 label이 일치해야한다 안그러면 만들어지지 않는다 <br>
셀렉터는 레이블 하나는 해줘야함 <br>
직접 지워보면서 실습하면된다 <br>
```yaml
apiVersion: v1

kind : ReplicationController
metadata:
  name : http-go
  labels:
    app : http-go
    env : dev

spec:
  replicas: 3
  selector:
    app : http-go
  template:
    metadata:
      name: http-go
      labels:
        app : http-go
    spec:
      containers:
        name : http-go
        image : gasbugs/http-go
        ports :
          containerPort : 80
```


#### 스케일링 3가지 방법
급한경우는 1번이고 문서화시킬려면 3번 방법이 제일좋은 것 같다<br>
- kubectl scale rc <이름> replicas= 3
- 직접 파일 들어가서 변경하기
- kubectl apply -f http-go-rc-v2.yaml 이렇게 다른걸로 적용시키기 이러면 스스로 조절해준다는게 신기

#### 레플리카 셋
```
레플리케이션 컨트롤러는 레이블에대한 선택을 유연하게 못했는데
레플리카 셋은 이러한 한계를 보완했다.
일반적으로 key value가 딱맞아야하지만 표현식이 생겼다.
```


![image](https://github.com/cwangg897/learning/assets/79621675/372a0c57-9eaa-4474-918a-8344b70a5445)

#### 실습
```yaml
apiVersion : app/v1
kind : ReplicaSet

metadata:
  name : rs-nginx
  labels:
    app : guestbook
spec:
  replicas: 3

  selector:
    matchLabels:
      app : rs-nginx
  template:
    metadata:
      name : rs-nginx
      labels:
        app : guestbook
    spec:
      containers:
        image : nginx
        ports:
          containerPort: 80

kubectl scale rs rs-nginx replicas = 10
```

