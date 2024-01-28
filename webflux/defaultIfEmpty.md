### defaultIfEmpty 위치에 상관있는가?
defaultIfEmpty는 스트림에 아이템이 없을 때 사용되며, filter 바로 아래에 위치하든 그렇지 않든 동일한 결과를 얻을 수 있습니다. 
filter 이후에 남은 아이템이 없다면 defaultIfEmpty는 적용되어 디폴트 값을 제공할 것입니다.


```java
    public Mono<TransactionResponseDto> createTransaction(TransactionRequestDto request){
        return userRepository.updateUserBalance(request.getUserId(), request.getAmount())
                .filter(Boolean::booleanValue) // successful인경우만 기록
                .map(value -> EntityDtoUtil.toEntity(request))
                .flatMap(userTransactionRepository::save)
                .map(ut -> EntityDtoUtil.toDto(request, TransactionStatus.APPROVED))
                .defaultIfEmpty(EntityDtoUtil.toDto(request, TransactionStatus.DECLINED));
    }
```
