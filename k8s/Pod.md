### 파드
```
포드는 안에 다수의 컨테이너 포함되어있음
단일 노드에서만 실행 - 파드는 하나의 노드에서만 실행된다
포드의 장점은 밀접하게 연관된 프로세스를 하나의 환경에서 동작하는 것처럼보이지만 격리된 상태로 유지
외부의 서비스할려면 서비스로 만들어야함 (expose)
일반적으로 포드하나에 프로세스(애플리케이션)하나를 권장함 스케일링 가능하게 - 밀접하다면 한곳에 넣지만
```


### yaml로 파드 디스크립터 만들기
```
버전관리가 편리하다
kubectl실행 명령어로 간단한 리소스 작성 방법도 가능하지만, 일부 항목에 대해서만 가능하니까 저장이 용이하지 않음
모든 쿠버네티스 객체를 YAML로 정의하면 버전 제어가 가능하다
공식문서를 참고해보자
```

### yaml에서 포드를 어떻게 정의하는가? 
- apiVersion : 쿠버네티스의 api의 버전을 가리킴
- kind : 어떤 리소스 유형인지 (포드 레플리카 컨트롤러, 서비스 등)
- 메타데이터 : 포드와 관련된 이름, 네임스페이드, 라벨 등등 정보
- 스펙 : 컨테이너, 볼륨 등의 정보
- 상태 : 포드의 상태, 각 컨테이너의 설명 및 상태, 포드 내부의 IP및 그 밖의 기본 정보 등 (이거는 알아서 작성해줌)
  

#### 연습문제
![image](https://github.com/cwangg897/learning/assets/79621675/2bb5d296-95ae-49a2-9f62-2b4202976528)
```
kubectl이 docker랑 같다고 생각
1. kubectl delete pod --all
2.
apiVersion : v1
kind : pod
metadata:
  name : jenkins-manual
spec:
  containers:
  - name : jenkins
    image : jenkins/jenkins:lts
    ports : 
    - containerPort : 8080
  
3. kubectl exec jenkins-manual --curl 127.0.0.1:8080 -s (컨테이너 내부에 들어가서 명령어를 실행하라)
4. kubectl port-forward jenkins-manual 8888:8080
5. kubectl get pod jenkins-manual -o yaml
```


### 라이브니스, 레디네스 프로브 구성 (파드의 보조역할들)

#### Liveness Probe
```
라이브니스 프로브은
컨테이너가 살았는지 판단하고 만약 살아있지 않다면 다시 시작하는 기능
컨테이너의 상태를 스스로 판단하여 교착 상태에 빠진 컨테이너를 재시작
버그가 생겨도 높은 가용성을 보임
```

#### Readiness Probe
```
포드가 준비된 상태에 있는지 확인하고 정상 서비스를 시작하는 기능(준비상태를 보고 시작)
포드가 적절하게 준비되지 않은 경우 로드밸런싱을 하지 않음 (휴지기간 같은거인듯)
```

#### Startup Probe
![image](https://github.com/cwangg897/learning/assets/79621675/a1bc8831-998a-4892-aed8-faf2ab4a64bf)
```
애플리케이션의 시작 시기 확인하여 가용성을 높이는 기능
Liveness와 Readiness의 기능을 비활성화 스스로 컨테이너가 시작되는 시간을 벌어주는것
컨테이너 시작할때 2개의 기능을 활성하면 시간이 오래걸림
시작에 대한 시간을 보장해주는거 시작시간동안
컨테이너를 체크하면서 살아있다고 판단하면 라이브니스와 리드니스가 동작
만약 정상시작아닌데 라이브니스 검사해서 재시작하면 문제생기고 레디니스는 상관없지만 시작도아닌데 검사하니까 비효율적임
```


#### 실습
![image](https://github.com/cwangg897/learning/assets/79621675/e334c401-641e-4a76-9bc2-f0231b64011f)<br>
공식문서에 liveness probe라고 검색하면됨 <br>
<https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/> <br>



