
[[Redis Docker 이용해서 띄우기]]

[Spring Data Redis 공식](https://docs.spring.io/spring-data/redis/reference/redis/getting-started.html)
[Spring boot에서 Redis로 캐싱하기 (w. JPA)](https://velog.io/@juhyeon1114/Spring-boot%EC%97%90%EC%84%9C-Redis%EB%A1%9C-%EC%BA%90%EC%8B%B1%ED%95%98%EA%B8%B0-w.-JPA)

Spring Data Redis는 **Redis 2.6이상**이 필요하고 Java 라이브러리인 **Lettuce와 Jedis와 통합된다.**

RedisConnection 클래스는 스레드 안전하지 않다.
- 기본 네이티브 연결 Lettruce의 StatefulRedisConnection은 스레드에 안전할 수 있다.
- 하지만 Spring Data Redis의 LettuceConnection 클래스 자체는 그렇지 않다.
여러 스레드에서 RedisConnection의 인스턴스를 공유해서는 안된다.


[Connection Modes](https://docs.spring.io/spring-data/redis/reference/redis/connection-modes.html)
## Redis의 HA(고가용성)을 구성하는 방법
- 아래 두 기술 모두 하나의 Redis가 아닌 여러 Redis를 하나의 Redis처럼 사용할수 있게 해주는 기술 

[Redis Sentinel vs Cluster](https://jojaeng2.tistory.com/40)
### Redis-Sentinel
- Master-Slave 방법
	- Master가 다운되면 이를 감지해 Slave 를 마스터로 올리고 클라이언트들이 새로운 Master에 접속할 수 있도록 해준다.
### Redis-Cluster
- 저장 잧리를 여러개 동시에 사용하고 마치 하나의 저장소처럼 사용하는 방법

[RestTemplate](https://docs.spring.io/spring-data/redis/reference/redis/template.html)

템플릿에서 쓰거나 읽는 모든 객체는 Java를 통해 직렬화되고 역직렬화된다.