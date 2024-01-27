### 동기 메소드 (void 반환형)
```java
Copy code
public void deleteById(String id) {
    productRepository.deleteById(id);
}
```
위 코드는 deleteById 메소드가 void를 반환합니다. 이는 메소드가 동기적으로 실행되고, 삭제 작업이 완료되면 그냥 메소드가 종료되고 반환값이 없음을 의미합니다. 
이 경우에는 삭제 작업이 완료되었는지에 대한 정보를 호출자에게 알려주지 않습니다.



### 비동기 메소드 (Mono<Void> 반환형)
```java
public Mono<Void> deleteById(String id) {
    return productRepository.deleteById(id);
}
```
여기서는 deleteById 메소드가 Mono<Void>를 반환합니다. 이는 리액티브 방식으로 동작하며, 삭제 작업이 비동기적으로 수행됩니다. 
반환된 Mono<Void>는 비동기 작업이 완료되면 완료 신호를 방출하게 됩니다. 
호출자는 이 Mono를 구독(subscribe)하여 삭제 작업이 완료될 때까지 기다릴 수 있습니다.

호출자(또는 구독자)는 리액티브 시스템의 이점을 살려서 비동기 방식으로 작업이 완료될 때까지 블로킹되지 않으면서,
또는 리액티브 스트림의 연산자를 사용하여 작업이 완료되었을 때 추가적인 로직을 수행할 수 있습니다.
따라서 리액티브 환경에서는 Mono<Void>를 반환하여 비동기적으로 작업을 수행하고, 완료 여부를 구독자에게 알리는 것이 일반적입니다.



### 몽고atlas헷갈린점
우리가 빌린것은 몽고db이다
그래서 안에 데이터베이스를 생성해주고 컬렉션도 만들어줘야한다
![image](https://github.com/cwangg897/learning/assets/79621675/29454710-bf8b-43e4-bf3a-aeb0f110791e)
