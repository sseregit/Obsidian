[[Spring Boot 2.* to 3.*]]에서 만든 프로젝트에 JWT를 적용하기.

메인이 될 참고 자료
[스프링부트 JUnit 테스트 - 시큐리티를 활용한 Bank 애플리케이션](https://github.com/codingspecialist/junit-bank-class)

참고자료
[spring security sample - JWT](https://github.com/spring-projects/spring-security-samples/tree/main/servlet/spring-boot/java/jwt/login)
[[Spring] Spring Security를 이용한 로그인 구현 (스프링부트 3.X 버전) [4] - JWT를 이용한 인증](https://velog.io/@dh1010a/Spring-Spring-Security%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EA%B5%AC%ED%98%84-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-3.X-%EB%B2%84%EC%A0%84-4-JWT%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%9D%B8%EC%A6%9D)
[Spring Security OAuth2로 JWT 검증하기](https://velog.io/@hong1008/spring-oauth-jwt)
[JWT 인증 작동 방식](https://docs.spring.io/spring-security/reference/servlet/oauth2/resource-server/jwt.html#oauth2resourceserver-jwt-architecture)

변경하면서 생각해야 할것들
1. 로그인 로그아웃 로그
2. 메뉴접근 로그

작업
1. 의존성 변경
```groovy
implementation "org.springframework.boot:spring-boot-starter-oauth2-client"

implementation "org.springframework.boot:spring-boot-starter-oauth2-resource-server"
```
- 둘의 차이점은 oauth2를 사용하는 클라이언트냐 리소스 서버이냐 의 차이
- JWT를 구현해서 사용하려면 resource-server로 충분하다.

2. 설정 변경