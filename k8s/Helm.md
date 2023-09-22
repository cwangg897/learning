#### HelmCahrt란
```
yaml을 일일히 하는것은 많은 노력이 들어간다
애플리케이션 하나 배포하는데 yaml많이 구성해야하기때문에 시간이 걸린다
Helm차트는 여러가지 yaml이 필요한것을 하나의 패키지로 미리만들어 놓는것을 이야기합니다
그래서 의존성도 만들고 필요한 Secret이나 이런것을 자동으로 구성해서
Helm을 사용하는 사용자가 쿠버네티스에 애플리케이션을 배포하기 쉽게 도와준다
모니터링 파트에 가장많이 사용된다
```

#### 설치방법
```
Kubectl이 설치된곳에 설치해야하는데
GCP를 이용하면 이미 Helm이 설치되어있다
```

#### Helml
```
Helm은 외부에서 정의된 yaml파일을 내려 받아 쿠버네티스에 애플리케이션을 배포한다
apt, yum과 같이 저장소를 별도로 두고 있다
외부 저장소를 helm repo add 명령으로 추가한다
bitnami안에는 엄청맣은 이미지가 들어있다
```


#### GKE 실습
```
helm repo add bitnami https://charts.bitnami.com/bitnami (저장소 추가하기)
helm repo update (저장소 가져온거 내거에 적용하기)
관리하기편하려면 네임스페이스를 생성
# 네임스페이스 생성 
kubectl create ns mysql

# 헬름 차트로 mysql 배포
helm install mysqlname bitnami/mysql -n mysql
```


#### Helm차트에서 새로운 차트 생성과 실행
```
나만의 차트를 통해서 내 애플리케이션 배포 환경을 만드는것
helm create mychart (내 차트만듬)
경로에 대한 학습이되어야함
mychart만들면 디렉토리 하나 생성됨 여기안에 구성요소 보고 가서 내걸로 구성하기
Chart.yaml 에 description보면 설명부분을 넣어주면됨
mysql비번은 무엇이고 이런거 
예를들어 mysql헬름차트를만들면 mysql비번 설명이랑 appVersion은 mysql버전이런거 명시하기

그다음 중요한 부분은 templates디렉토리의 deployment 등등
그래서 내가 수정해야하는부분은 values파일이다
helm install mychart(차트이름) ./mychart/ 이러면 레포지토리없이 애플리케이션을 배포가능
이런거를 이제 레포지토리에 넣어서 추가해서 배포하는거인듯 
```

#### 차트추가후 다운
```
차트 내가 만들어서 깃허브로 배포하고 Helm차트로 깃허브레포지토리 추가해서 install해서 사용하기



```


#### 느낀점
쿠버네티스가 오케스트레이션이라고 느낀것은 마스터에서 워커노드들을 클러스터로 구성하고 관리하기때문이다. <br>
어찌보면 AWS서비스를 쿠버네티스 용어로 풀어쓴것이고 매칭된다. <br>

