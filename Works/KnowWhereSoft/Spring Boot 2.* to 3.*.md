[Spring-Boot-3.0-Migration-Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide)
[Spring-Security-6.0-Migration-Guide](https://docs.spring.io/spring-security/reference/6.0/migration/index.html)
[Spring-Framework 6.x로 업그레이드](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x)
[Migration support in IntelliJ IDEA](https://blog.jetbrains.com/idea/2021/06/intellij-idea-eap-6/).

1. 최신 Spring-Boot 2.7.x를 파악해야 하고 가장 최신 버전으로 업그레이드를 먼저 해야한다.
2. 스프링 시큐리티를 사용할 경우
	1. Spring Boot 3.0은 Spring Security 6.0을 사용한다.
	2. Spring Security는 6.0을 업그레이드를 단순화 하기 위해 Spring Security 5.8을 출시
	3. 업그레이드 하기전 Spring Security 5.8로 업그레이드.
3. 요구 사항
	1. Spring Boot 3.0
		1. Java 17 이상 
		2. Spring Framework 6.0
4. 구성 속성 마이그레이션
`runtime("org.springframework.boot:spring-boot-properties-migrator")`
- 마이그레이션 완료되면 종속성에서 모듈 제거
5. Spring-Framework 6.x로 업그레이드 참고
6. 