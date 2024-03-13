## 참고 URL
[Spring-Boot-3.0-Migration-Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide)
[Spring-Security-6.0-Migration-Guide](https://docs.spring.io/spring-security/reference/6.0/migration/index.html)
[Spring-Framework 6.x로 업그레이드](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x)
[Migration support in IntelliJ IDEA](https://blog.jetbrains.com/idea/2021/06/intellij-idea-eap-6/)
[Intellij javax => jakarta Migration ](https://www.jetbrains.com/guide/java/tutorials/migrating-javax-jakarta/use-migration-tool/)
[Hibernate-6.1-Migration-Guide](https://docs.jboss.org/hibernate/orm/6.1/migration-guide/migration-guide.html)
[Gradle 변경사항](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide#gradle-changes)
[Spring Boot Gradle 플러그인 참조 가이드](https://docs.spring.io/spring-boot/docs/3.0.x/gradle-plugin/reference/htmlsingle/)

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
- Version을 직접 명시한 리스트
	- plugins
		- `id 'org.springframework.boot' version '2.7.7'`
		- `id "com.ewerk.gradle.plugins.querydsl" version "1.0.10"`
		- `id 'org.asciidoctor.jvm.convert' version '3.3.2'`
		- `id "io.spring.dependency-management" version '1.1.0'`