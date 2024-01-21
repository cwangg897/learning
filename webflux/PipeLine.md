
### Bad Practice
이러면 브라우저에서 취소해도 취소가 안됨 위에 코드는 Reactive가 아니라서
결론은 method pipeline을 이용하자
```java

    public Flux<Response> multiplicationTable(int input){
        List<Response> list =  IntStream.rangeClosed(1, 10)
                .peek(i -> {
                    SleepUtil.sleepSeconds(1);
                })
                .peek(i -> System.out.println("math-service processing : " + i))
                .mapToObj(i -> new Response(i * input))
                .collect(Collectors.toList());
        return Flux.fromIterable(list); 
    }
```
