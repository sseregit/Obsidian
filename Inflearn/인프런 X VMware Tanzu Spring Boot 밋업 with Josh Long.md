
### opcode에서 switch는 if보다 훨씬 낫다
 - switch는 오프셋으로의 상수 시간 점프이기 때문이다.

### temporal coupling (시간적 결합)
### locational coupling (위치적 결합)
```java
@Async
@EventListener
void ....() {
	...
}
```
- 비동기 처리로 위에 문제를 해결
- 하지만 하나의 프로세스가 완성되야 완성인데 해당 스레드가 돌때 문제가 생길수 있는 문제가 생긴다.
```java
@ApplicationModuleListener // (@Async + @Transactional + @EventListener)
void ....() {
	...
}
```
- Spring Moduleth 추가 필요