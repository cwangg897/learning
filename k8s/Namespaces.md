#### 네임스페이스
```
권한을 나눠서 자신만의 공간에 원하는 포드자원들을 배치하고 통신시킬수록 되어있음
자원을 한정되게해서 좀더 안정적이고 많은사람들이 사용할수있는 서비스만들어줌
- 리소스를 각각의 분리된 영역으로 나누기 좋은 방법 (스페이스)
- 여러 네임스페이스를 사용하면 복잡한 쿠버네티스 시스템을 더 작은 그룹으로 분할
- 멀티 테넌트(Multi-tenant)환경을 분리하여 리소스를 생산, 개발, QA 환경 등으로 사용
- 리소스 이름은 네임스페이스 내에서만 고유 명칭 사용 (다른공간에서 같은이름 가능)

현재 클러스터의 기본 네임스페이스 확인하기 kubectl get ns

만약 CD할때 개발환경 배포 하고 그런식으로 가능하구나

```

#### 네임스페이스 만들기
```yaml
apiVersion: v1

kind : Namespace

metadata:
  name: test-ns
```

#### 자원 할당
```
kubectl run nginx --image nginx -n <이름> [자원할당 방법]

kubectl get all -n office[조회 하는방법]
kubectl get all -all -namespaces [전체 네임스페이스 조회]
kubectl delete ns office [네임스페이스 지우기 안에내용도 다 사라짐]
```

#### 연습문제 
![image](https://github.com/cwangg897/learning/assets/79621675/436f002c-f493-418a-862c-ae4e13f786da)
```
kubectl get ns [네임스페이스 목록]
kubectl get ns | wc -l [파이프라인으로 몇개가있는지 볼 수 있음]
kubectl get pod -n kube-system [네임스페이스에 파드 리스트]

kubectl get pod --all-namespaces  |  grep coredns [모든 파드의 네임스페이스가 나옴]
```

할당방법
```yaml
apiVersion: apps/v1
kind : Namespace
metadata:
  name: jenkins-ns


---

apiVersion: v1
kind : Pod
metadata:
  name : jenkins-app
  namespace : jenkins-ns
spec:
  containers:
    image : jenkins
    name : jenkins
    ports:
      containerPort : 8080
```
