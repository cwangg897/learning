#### 디플로이먼트
- 애플리케이션을 다운 타임 없이 업데이트 가능하도록 도와주는 리소스
- 레플리카셋과 레플리케이션컨트롤러 상위에 배포되는 리소스 (버전업데이트 도우미)

#### 모든 포드를 업데이트하는 방법
- 잠깐의 다운 타임 발생하는 (re-create) 새로운 포드를 실행시키고 작업이 완료되면 오래된 포드를 삭제 하는방법 (삭제되고올라오기때문에)
- 롤링 업데이트 (낮은 버전하나씩 교체한느거)
- 
#### 실습
![image](https://github.com/cwangg897/learning/assets/79621675/a0714dc8-3f4e-4a72-a87d-5ee02d07e8e4)

```yaml
apiVersion: apps/v1

kind : Deployment

metadata:
  name : deploy-jenkins
  labels:
    app: jenkins-test

spec:
  replicas: 5
  selector:
    matchLabels:
      app: jenkins-test
  template:
    metadata:
      name : deploy-jenkins
      labels:
        app: jenkins-test
    spec:
      containers:
        image : jenkins
        name : jenkins
        ports:
          containerPort: 8080
```

