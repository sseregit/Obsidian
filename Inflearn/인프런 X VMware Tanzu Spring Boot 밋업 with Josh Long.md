
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

### Spring Moduleth
- module ~= package

### Java는 기본적으로 모든 것을 public으로 만들지 않는다!
- 모든것이 public일 필요가 없고 캡슐화가 필요하다 

### 가상스레드
- 기본적으로 런타임이 블락킹을 일으키는 요청을 감지하면, 코드를 스레드에서 분리해 RAM으로 옮기고, 실제 스레드를 스레드 풀에 돌려보내어 다른 사람이 사용할 수 있도록 해준다.

[https://httpbin.org/]https://httpbin.org/
- HTTP 테스트에 유용하다

### GraalVM
- 네이티브 이미지 컴파일러
	- Mac, Linux, Windows의 네이티브 바이너리를 구축할 수 있다.
	- JDK, JRE, 런타임도 필요 없다
- 단점
	- 런타임에 모든 동적 동작에 대해 알려줘야 한다.
	- 네이티브 이미지 컴파일의 시간이 매우 오래 걸린다.