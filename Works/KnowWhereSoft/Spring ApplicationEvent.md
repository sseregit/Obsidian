[Spring 공식](https://docs.spring.io/spring-framework/reference/core/beans/context-introduction.html#context-functionality-events)

```kotlin
class TargetLogEvent(  
    source: Any,  
    val target: TargetEntity  
) : ApplicationEvent(source) {  
}
```

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
