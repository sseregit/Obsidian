## 참고 URL
- 공식 문서
[Spring-Boot-3.0-Migration-Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide)
[Spring-Security-6.0-Migration-Guide](https://docs.spring.io/spring-security/reference/6.0/migration/index.html)
[Spring-Framework 6.x로 업그레이드](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x)
[Migration support in IntelliJ IDEA](https://blog.jetbrains.com/idea/2021/06/intellij-idea-eap-6/)
[Intellij javax => jakarta Migration ](https://www.jetbrains.com/guide/java/tutorials/migrating-javax-jakarta/use-migration-tool/)
[Hibernate-6.1-Migration-Guide](https://docs.jboss.org/hibernate/orm/6.1/migration-guide/migration-guide.html)
[Gradle 변경사항](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide#gradle-changes)
[Spring Boot Gradle 플러그인 참조 가이드](https://docs.spring.io/spring-boot/docs/3.0.x/gradle-plugin/reference/htmlsingle/)
- 마이그레이션 관련 블로그
[스프링 부트 3.0 으로 전환](https://post.dooray.io/we-dooray/tech-insight-ko/back-end/4173/)
[스프링 부트 2에서 스프링 부트 3로 업그레이드 가이드](https://covenant.tistory.com/279)

## 작업
1. [Spring-Boot 2.7.* 의 최근 버전을 파악한다.](https://spring.io/projects/spring-boot#learn)
2. [Spring-Security 5.8.* 의 최근 버전을 파악한다.](https://spring.io/projects/spring-security#learn)
3. [Configuration Properties Migration](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide#configuration-properties-migration)
	1. application.properties의 대한 마이그레이션인데 application.yml을 사용할 경우도 작동하는지 파악이 필요하다.
4. [jakarta EE로 종속성 변경](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide#jakarta-ee)
	1. [Migration support in IntelliJ IDEA](https://blog.jetbrains.com/idea/2021/06/intellij-idea-eap-6/).
		1. 해당 도구를 참고해서 작업할 것.

CheckList
- Gradle Version 확인
	- 적용 할 Java Version이 잘 맞는지 확인
	- 7.3 버전 이후부터 Java 17 적용가능.
![[Pasted image 20240313143838.png]]
- QueryDSL classfiler jakarta로 변경해줘야함.
	- `implementation 'com.querydsl:querydsl-jpa:5.0.0:jakarta'`
- Java EE to Jakarta
	-  제외
		- javax.persistence.*
		- javax.servlet.*
		- **스프링부트와 스프링프레임워크가 버전이 올라가면 달라질수 있음.**
		- javax.sql,javax.crypto._ 패키지는 jakarta로 변화가 없습니다. Java EE에서 제공하는 패키지가 아닌 JDK 에서 제공하는 패키지이기 때문입니다.
- 직접 버전이 명시 되어 있는 종속성 체크하기
	- [종속성 버전](https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html#appendix.dependency-versions)
	- `implementation group: "commons-codec", name: "commons-codec", version: "1.9"`
		- 있음
	- `implementation group: "commons-io", name: "commons-io", version: "2.13.0"`
		- 버전업
	- `implementation "jdbc.tibero:tibero:6"`
		- 관련없음
	- mapstruct
		- java 17과 관련 없음
```groovy
annotationProcessor "org.projectlombok:lombok-mapstruct-binding:0.2.0"  
implementation "org.mapstruct:mapstruct:1.5.3.Final"  
annotationProcessor "org.mapstruct:mapstruct-processor:1.5.3.Final"
```
- `implementation 'com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.8.1'`
	- 버전업 
- implementation ('org.springdoc:springdoc-openapi-ui:1.6.6'){  
    exclude group: 'com.fasterxml.jackson.dataformat', module:'jackson-dataformat-yaml'}
	- spring boot 3 에서는 2버전을 사용해야한다.
- `implementation 'com.fasterxml.jackson.dataformat:jackson-dataformat-yaml:2.13.2'`
	- 있음
- `implementation 'org.dhatim:fastexcel:0.15.6'`
- `implementation 'org.dhatim:fastexcel-reader:0.15.6'`
	- 최신 버전으로 변경
- `implementation 'org.apache.poi:poi:5.2.3'`
	- 지원한다 최신버전으로 변경
- `implementation 'org.apache.poi:poi-ooxml:5.2.3'`