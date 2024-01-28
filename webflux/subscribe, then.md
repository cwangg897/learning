### subscribe
```
subscribe가 없으면 리액티브프로그래밍 즉 로직이 실행안된다.
그런데 우리의 서비스로직은 어찌동작하는거지? subscribe가없는데...
프레임워크가 동작한다.
```
<https://timewizhan.tistory.com/entry/Reactive-Web-Application%EC%9D%80-%EC%96%B8%EC%A0%9C-subscribe%EB%A5%BC-%ED%95%A0%EA%B9%8C>

### then
then(): 모든 작업이 완료되면 Mono<Void>를 생성하여 완료 신호를 보냅니다. 반환 값이 Mono<Void>이므로, 완료 신호만이 관심 있는 경우 사용합니다.
이 코드는 비동기적인 리액티브 프로그래밍 모델을 사용하여 계좌 조회, 업데이트, 이벤트 생성 및 저장 등을 처리합니다. 코드의 특징은 모든 단계가 비동기적으로 동작하며, 각 단계에서 에러가 발생하면 해당 에러를 처리하고 최종적으로 완료 신호를 반환하는 점입니다.




