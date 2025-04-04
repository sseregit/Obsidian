```java

public interface ProductRepository extends MongoRepository<ProductEntity, String> {
....
}

build.gradle
implementation 'org.springframework.boot:spring-boot-starter-data-mongodb'
```

리액티브 사용법
```java

public interface ProductRepository extends ReactiveMongoRepository<ProductEntity, String> {
....
}

build.gradle
implementation 'org.springframework.boot:spring-boot-starter-data-mongodb-reactive‘
```

implementation을 
`implementation 'org.springframework.boot:spring-boot-starter-data-mongodb'`를 유지한 상태에서 `ReactiveMongoRepository` 를 만들면 빈등록조차 안된다.