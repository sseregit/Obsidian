[Spring 공식](https://docs.spring.io/spring-framework/reference/core/beans/context-introduction.html#context-functionality-events)
[spring 이벤트 사용하기(event publisher, event listener)](https://wildeveloperetrain.tistory.com/217)

```kotlin
class TargetLogEvent(  
    source: Any,  
    val target: TargetEntity  
) : ApplicationEvent(source) {  
}
```
- 공식 홈페이지 6.1.12 기준의 있을때는 상속하는 구조를 사용하는거 처럼 적혀 있는데 4.2버전 이후로는 상속하지 않아도 사용이 가능하다고 한다.
	- 그 이유는 `default void pulishEvent(Application event)` 였는데 `void publishEvent(Object event)`가 추가 되었고 이 메서드를 호출하기 때문에 상속을 할 필요가 없다.


```kotlin
@Component
class TargetLogNotifier: ApplicationListener<TargetLogEvent> {

    val log = logger()

    override fun onApplicationEvent(event: TargetLogEvent) {
        log.info("========= ApplicationListener 시작 =========")
        log.info(event.target.toString())
        log.info("========= ApplicationListener 종료 =========")
    }
}
```

```kotlin
@Service
class TargetLogService : ApplicationEventPublisherAware {
    private lateinit var publisher: ApplicationEventPublisher

    var log = logger()

    override fun setApplicationEventPublisher(publisher: ApplicationEventPublisher) {
        this.publisher = publisher
    }

    fun createTargetEntityLog(targetEntity: TargetEntity) {
        log.info("========= ApplicationEventPublisherAware 시작 =========")
        publisher.publishEvent(TargetLogEvent(this, targetEntity))
        log.info("========= ApplicationEventPublisherAware 종료 =========")
    }

}
```

### 사용법
내가 사용하고 싶은 객체에서 `ApplicationEventPublisher`를 주입받아서
`publisher.publishEvent(ApplicationEvent를 구현한 클래스)`를 넣어주던가

`ApplicationEventPublisherAware`를 구현한 클래스를 주입받아 해당 메서드를 호출하는 식으로 사용한다.
