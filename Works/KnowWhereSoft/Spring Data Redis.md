
[[Redis Docker 이용해서 띄우기]]

[Develop with Redis](https://redis.io/docs/latest/develop/)
[Spring Data Redis 시작하기](https://redis.io/learn/develop/java/redis-and-spring-course)
[Spring Data Redis 공식](https://docs.spring.io/spring-data/redis/reference/redis/getting-started.html)
[Spring boot에서 Redis로 캐싱하기 (w. JPA)](https://velog.io/@juhyeon1114/Spring-boot%EC%97%90%EC%84%9C-Redis%EB%A1%9C-%EC%BA%90%EC%8B%B1%ED%95%98%EA%B8%B0-w.-JPA)

Spring Data Redis는 **Redis 2.6이상**이 필요하고 Java 라이브러리인 **Lettuce와 Jedis와 통합된다.**

RedisConnection 클래스는 스레드 안전하지 않다.
- 기본 네이티브 연결 Lettruce의 StatefulRedisConnection은 스레드에 안전할 수 있다.
- 하지만 Spring Data Redis의 LettuceConnection 클래스 자체는 그렇지 않다.
여러 스레드에서 RedisConnection의 인스턴스를 공유해서는 안된다.

## Redis

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

[Redis Cache](https://docs.spring.io/spring-data/redis/reference/redis/redis-cache.html)

[Hash Mapping](https://docs.spring.io/spring-data/redis/reference/redis/hash-mappers.html)

[Pub/Sub Messaging](https://docs.spring.io/spring-data/redis/reference/redis/pubsub.html)

[Redis Stream](https://docs.spring.io/spring-data/redis/reference/redis/redis-streams.html)

[Redis Transactions](https://docs.spring.io/spring-data/redis/reference/redis/transactions.html)
- 기본적으로 RestTemplated은 관리되는 Spring 트랜잭션에 참여하지 않는다.
- 트랜잭션 또는 트랜잭션 템플릿을 사용할 때 RedisTemplate이 Redis 트랜잭션을 사용하도록 하려면 명시적으로 setEnableTransactionSupport(True)를 설정해야 한다.
- Redis 트랜잭션은 배치 지향적이다.
- 트랜잭션중 실행된 명령은 큐에 대기하고 트랜잭션을 커밋할 때만 적용된다.

[Pipelining](https://docs.spring.io/spring-data/redis/reference/redis/pipelining.html)

## Redis Repositories

[Usage](https://docs.spring.io/spring-data/redis/reference/redis/redis-repositories/usage.html)

도메인 엔티티를 구현하는 방법


## 코딩해보기
[spring-data-redis-tutorial](https://www.baeldung.com/spring-data-redis-tutorial)
[Spring Data Redis Repository 미숙하게 사용해 발생한 장애 극복기](https://hyperconnect.github.io/2022/12/12/fix-increasing-memory-usage.html)
[Redis 소개](https://inpa.tistory.com/entry/REDIS-%F0%9F%93%9A-%EA%B0%9C%EB%85%90-%EC%86%8C%EA%B0%9C-%EC%82%AC%EC%9A%A9%EC%B2%98-%EC%BA%90%EC%8B%9C-%EC%84%B8%EC%85%98-%ED%95%9C%EB%88%88%EC%97%90-%EC%8F%99-%EC%A0%95%EB%A6%AC?category=918728#redis-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0---%EC%BA%90%EC%8B%9Ccache)
[Redis Cache 전략](https://inpa.tistory.com/entry/REDIS-%F0%9F%93%9A-%EC%BA%90%EC%8B%9CCache-%EC%84%A4%EA%B3%84-%EC%A0%84%EB%9E%B5-%EC%A7%80%EC%B9%A8-%EC%B4%9D%EC%A0%95%EB%A6%AC)

## 목표
1. Spring-data-Redis 사용법 익히기
2. Redis-Sentinel 설정
	1. docker 사용방법
	2. local 사용방법

```java
    @Bean
    public RedisConnectionFactory connectionFactory() {
        return new LettuceConnectionFactory();
    }

```
대부분의 예제코드들이 이렇게 생성자만 호출할 수 있는 이유는 localhost에 6379포트 설정이 default이기 때문이다.
```yaml
spring:
    redis:
        host: 127.0.0.1
        port: 6379
```
자동으로 등록하는 방법도 있다.

저장한 값은 Hash로 저장한다!!
redis-cli - Hash의 기본명령어

이미 존재하는 키로 save를 호출할 경우에는 해당 키가 의 value들이 update 된다.

@Transactional이 필요한가????? 필요하다면 왜...?...사용법

기본적으로 Redis 문자열은 최대 512MB가 될 수 있다.

@Indexed
- 해당 필드의 키:필드 라는 키가 생기고 값은 @Id의 필드가 된다.
- @Indexed 를 조회하는 findByName()같은 메서드를 만들면
	- 키:필드:입력값 으로 @Id를찾고
	- 찾은 Id로 다시 조회를해서 값을 가져온다.

개발환경에 Redis를 설치하기 위해 Sentinel방법을 찾는다.
[Failover Using Sentinel for Redis](https://junhyunny.github.io/spring-boot/redis/failover-using-sentinel-for-redis/)
[Spring Data Redis Sentinel](https://docs.spring.io/spring-data/redis/reference/redis/connection-modes.html#redis:write-to-master-read-from-replica)
[Redis Document Sentinel](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/)
[5분 안에 구축하는 Redis-Sentinel](https://co-de.tistory.com/15)
[Redis configuration](https://redis.io/docs/latest/operate/oss_and_stack/management/config/)
master-slave와 sentinel이 1:1로 각각 띄워져 있어야한다.
`redis-sentinel`은 구성파일이 필수이다.

redis-server를 먼저 띄운다
```
redis-server /path/to/redis.conf
```

redis-sentinel을 띄운다
```
redis-sentinel /path/to/redis-sentinel.conf
```
순서가 중요함

연결을 확인하는 방법
```
redis-cli -p (포트)

접속후
info sentinel

sentinel master (마스터명)

으로 확인한다.

SENTINEL replicas (마스터명)
SENTINEL sentinels (마스터명)

replica와 sentinel들을 확인할수 있는 명령어

SENTINEL get-master-addr-by-name (마스터명)
현재 마스터를 확인하는 API
```

죽이거나 딜레이를 주면 conf 파일 설정들이 바뀐다.
master가 된 포트는 
replicaof 127.0.0.1 (포트) 사라지고
master에서 replicas가 된 포트는
replicaof 127.0.0.1 (포트) 추가된다.

sentinel도 마찬가지고

런타임중에 Sentinel을 재구성 할 수 있다.

구성하는거 대충 알겠다
먼저 스프링에 적용해서 테스트 해보고
그다음에 운영에서 사용할 반드시 추가해야 하는 설정 찾아야 한다.

스프링 적용 부터

redis-cli monitor는 master slave가 변화할때 다 끊기는데

redis-cli는 살아있고 

DEBUG 경우
다시 살아 났을때도 문제없이 redis server의 데이터의 정합성이 맞는다.

Shutdown 경우
다시 살아나고 나서 바로 redis server의 정합성이 맞춰진다

다 죽을 경우 Redis command time out으로 서버가 죽을거 같은데?

여기 까지는 운영중에 redis-server가 죽은 경우고

이제는 redis-sentinel이 죽을 경우

