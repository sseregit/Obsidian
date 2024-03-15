## 참고 URL
- 공식 문서
[Spring-Boot-3.0-Migration-Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide)
[Spring-Security-6.0-Migration-Guide](https://docs.spring.io/spring-security/reference/6.0/migration/index.html)
[Spring-Security-Gradle Version Update 적용하는법](https://docs.spring.io/spring-security/reference/getting-spring-security.html#getting-gradle)
[Spring-Framework 6.x로 업그레이드](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x)
[Migration support in IntelliJ IDEA](https://blog.jetbrains.com/idea/2021/06/intellij-idea-eap-6/)
[Intellij javax => jakarta Migration ](https://www.jetbrains.com/guide/java/tutorials/migrating-javax-jakarta/use-migration-tool/)
[Hibernate-6.0-Migration-Guide](https://docs.jboss.org/hibernate/orm/6.0/migration-guide/migration-guide.html)
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


## 작업하기
1. spring-boot 2.7.{maxVersion} 으로 build
2. spring-security 5.8.{maxVersion}으로 build
	1. version 명시가 아닌 위 문서 참고
3. spring-boot 3.0 준비
	1. target version : 3.2.3
		1. [grale plugin io.spring.dependency-management 의 최신 버전을 확인한다.](https://plugins.gradle.org/plugin/io.spring.dependency-management)
		2. 해당 버전의 [Dependency Versions](https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html#appendix.dependency-versions)으로 버전이 명시되어 있는 종속성들이 나와 있는지 확인후 변경
		3. 없다면 찾아서 최신화
	2. Query DSL
		1. jakarta version으로 설정
	3. application.properties와 application.yml 업데이트를 위한 모듈 추가
		1. `runtime("org.springframework.boot:spring-boot-properties-migrator")`
		2. 마이그레이션이 완료되면 모듈 제거
	4. Intellij 컴파일러 version Java17로 변경
	5. build.gradle에 Java 버전 17로 변경
	6. import javax.* => import jakarta.*
4. 시련
	1. hibernate Custom function 방법이 달라졌다.
		1. [FunctionContributor](https://discourse.hibernate.org/t/migration-of-dialect-to-hibernate-6/6956)를 사용해야한다.
		2. 제대로 호출하는지 확인이 필요하다.
	2. querydsl
```groovy
implementation "com.querydsl:querydsl-jpa:${queryDslVersion}:jakarta"  
annotationProcessor "com.querydsl:querydsl-apt:${queryDslVersion}:jakarta"  
annotationProcessor "jakarta.annotation:jakarta.annotation-api"  
annotationProcessor "jakarta.persistence:jakarta.persistence-api"
```
- 최종 querydsl 종속성 추가 방법
	3. SecurityConfig
		1. 6.2.2 버전에 따라 메서드명 변경과 문법 변경 처리.
```java
@Bean  
@Order(0)  
public SecurityFilterChain resourceChain(HttpSecurity httpSecurity) throws Exception {  
    httpSecurity.requestMatchers((matchers)->matchers.antMatchers(staticResource()))  
		...
    return httpSecurity.build();  
}

// 아래 방법으로 변경

@Bean  
public WebSecurityCustomizer webSecurityCustomizer() {  
    return (web) -> web.ignoring().requestMatchers(staticResource());  
  
}  
```

- csrf
```java

http.csrf().ignoringAntMatchers("/auigrid/fileupload/*"  
        ,UrlFormat.PATH_REST_API_PREFIX+"/**","/**")  
        .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse());

// 아래로

http.csrf((csrf) -> csrf.ignoringRequestMatchers("/auigrid/fileupload/*",UrlFormat.PATH_REST_API_PREFIX+"/**","/**")        .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse()));  
  
```

- formLogin
```java
http.formLogin()  
        .loginPage(authenticationProperties.getLoginUrl()).permitAll()  
        .loginProcessingUrl(authenticationProperties.getLoginProcessUrl())  
        .usernameParameter(authenticationProperties.getUsername())  
        .passwordParameter(authenticationProperties.getPassword())  
        .successHandler(authenticationSuccessHandler(authenticationRepository, requestLogger))  
        .failureHandler(authnFailHandler(authenticationRepository));

// 아래로

http.formLogin((form) -> form.loginPage(authenticationProperties.getLoginUrl()).permitAll()  
                            .loginProcessingUrl(authenticationProperties.getLoginProcessUrl())  
                            .usernameParameter(authenticationProperties.getUsername())  
                            .passwordParameter(authenticationProperties.getPassword())  
                            .successHandler(authenticationSuccessHandler(authenticationRepository, requestLogger))  
                            .failureHandler(authnFailHandler(authenticationRepository)));  
```

- logout
```java
http.logout()  
        .logoutUrl("/logout")  
        .logoutSuccessUrl("/login")  
        .logoutSuccessHandler(new LogoutSuccessLogger(requestLogger))  
        .invalidateHttpSession(true)  
        .deleteCookies("JSESSIONID");

// 아래로

http.logout((logout) -> {  
    logout.logoutUrl("/logout")  
            .logoutSuccessUrl("/login")  
            .logoutSuccessHandler(new LogoutSuccessLogger(requestLogger))  
            .invalidateHttpSession(true)  
            .deleteCookies("JSESSIONID");  
})  
```

- exceptionHandling
```java
http.exceptionHandling((e) -> {  
    e.accessDeniedHandler(accessDeniedHandler(messageSource))  
     .authenticationEntryPoint(new AjaxAwareAuthenticationEntryPoint("/login"));  
});
```

- Mapstruct Builder를 못찾는 버그에 때문에 막혀있다.
- querydsl plugin제거 방법 찾기.
```groovy
def querydslDir = "$buildDir/generated/querydsl"  
tasks.withType(JavaCompile) {  
    options.getGeneratedSourceOutputDirectory().set(file(querydslDir))  
}  
// build 시 사용할 sourceSet 추가  
sourceSets {  
    main.java.srcDir querydslDir  
}
```
- gradle version 올리기
	- [7.X => 8.* 버전업](https://docs.gradle.org/current/userguide/upgrading_version_7.html)
	- 7.6.4로 변경
- querydsl plugin 제거와 함께 Mapstruct 버그가 사라짐.

- 빌드 완성

- Login 화면 띄우기
1. spring 시작전 logger와 관련된 로그가 console에 찍히고 시작됨.  
	1. [logback](https://logback.qos.ch/codes.html#nested_if_element)
	2. `<springProfile></springProfile>` 로나누었다
2. `database-platform: org.hibernate.dialect.OracleDialect`
	1. 이슈
	2. `implementation 'org.hibernate.orm:hibernate-community-dialects'`
		1. hibernate 6.0 version은 기본적으로 Oracle minumum 이 19 버전임.
3. create global temporary table 이슈 
	1. 다중 테이블 대량 작업을 위해 사용한다고 함.
4. security
	1. `You are asking Spring Security to ignore DispatcherServletDelegating`