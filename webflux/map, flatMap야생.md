### 언제map쓰고 언제 flatMap쓰는지 궁금
```
따라서, map은 현재 Mono에서 동기적인 변환을 수행할 때 사용되고, 
flatMap은 다른 비동기 작업을 호출하고 결과로 새로운 Mono를 생성할 때 사용됩니다. 
코드에서 flatMap을 사용하는 이유는 비동기 작업이 포함되어 있기 때문입니다.
```


```java
public Mono<ProductDto> insertProduct(Mono<ProductDto> dto){
        return dto.map(EntityDtoUtil::dtoToEntity)
                .flatMap(productRepository::insert)
                .map(EntityDtoUtil::entityToDto);

    }
```

### 그래서 그게 먼 차이인데?
동기적인 변환이란, 처리 과정에서 다른 작업을 기다리지 않고 즉시 진행되는 변환이라고 할 수 있습니다.
일반적으로 CPU 연산, 메모리 연산 등이 동기적으로 수행되는 예시입니다.
예를 들어, 숫자의 제곱을 계산하는 함수를 생각해봅시다. 이 함수는 동기적인 작업입니다.

```java
Copy code
public int square(int number) {
    return number * number;
}
```
위의 코드에서는 입력으로 받은 number를 바로 제곱하여 반환합니다. 
이 함수의 실행은 입력값에 대한 변환을 즉시 수행하며 다른 작업을 기다리지 않습니다.

이와 같이 동기적인 변환이 필요한 경우에는 map을 사용할 수 있습니다. 
예를 들어, Reactor의 Mono에서 map을 사용하여 동기적인 변환을 수행하는 코드는 다음과 같을 수 있습니다.

```java
Copy code
public Mono<Integer> square(Mono<Integer> mono) {
    return mono.map(number -> number * number);
}
```
위의 코드에서 map은 각 원소에 대해 동기적으로 변환을 수행합니다.
Mono의 각 원소가 동일한 유형을 유지하면서 변환되는 동안 flatMap은 다른 Mono를 반환할 수 있는 비동기 작업을 수행할 때 사용됩니다.

### 결론
DB기다리는 동안 다른작업이 가능한거 만약 여러개면 다른 디비또 호출하고 이런거를 말하나봄
