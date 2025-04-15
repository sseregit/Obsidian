# 1. 강의 소개
## 강의 소개
==Golang강의보다 더 자세히 다룬다..?!==
## Source Code

****
# 2. 프로젝트 구성하기
## initializer & dependencies build
==spring websocket을위한 의존성 추가 및 JPA, Lombok 등등...==
## yaml을 활용한 서버 환경 관리
==의존성에 필요한 설정과 JWT 토큰 관련 설정 작성==
## MySQL Transaction Manager Config
==TransactionManager에 대한 빈 등록과 Custom TransactionManager를 등록하는 방법==
**해당 강의의 DataSourceTransactionManager를 사용하는데 JPA를 사용하면 사실  JPA의 프록시를 이용한 기능들이 다 작동안함 LAZY, 영속성 컨텍스트로의 관리, dirty checking등등 JPA를 쓰는데 해당 TransactionManager를 사용하는건 치명적인 실수!!**
## HTTP와 웹소켓의 Configuration
==Security가 아닌 WebMvcConfigurer로 CORS와 WebSocketConfigurer로 WebSocket  소켓도 처음에 HTTP도 handshake를 하기 때문에 CORS와 비슷한 느낌의 설정을 가져간다.==
****
# 3. Auth에 대한 HTTP Router 작성하기
## Swagger & API에 대한 클래스 주입하기
==기본적인 Service, Model, Controller 작성 및 Swagger 정보도 작성==
## Entity와 Lazy Fetch에 관하여
==Entity 작성과 OneToOne에서 Lazy가아닌 eager fetch를 사용하는 이유와 Lazy에 대한 설명==
## JPA를 활용한 Service 구성하기
==JPARepository 만들고 Service에 유저 생성 로직 작성==
## SHA-256을 활용한 Password 해싱하기
==spring security에 bcrypt를 사용해서 core를 의존성 추가한줄 알았는데 패스워드에 대한 해싱을 `MessageDigest.getInstance(“SHA-256”)`으로 처리==
## RunTimeException에 대한 Customizing
==enum, interface를 조합해 CustomException을 핸들링 하는 방법==
## Auth API 기본적인 마무리하기
==보통 Spring Security로 이런 작업을 할테니 그렇게 좋은 방법은 아니지만 Spring Security를 사용해서 처리하더라도 보통 이런흐름으로 진행되니 상관없다.==
****
# 4. JWT에 대한 모든것
## 면접대비와 기능개발을 위한 JWT
==JWT의 이론과 [[JWT의 공개클레임? 비공개클레임?]]에 대한 것==
## JWT 설정을 위한 factory Annotaion 사용하기
==강의는 @Component와 setter의 @Value를 활용해 yml값을 바인딩하는데 나는 @ConfigurationPropertiesScan과 @ConfigurationProperties를 활용했다. 결과는 다르지 않다.==
## JWT Token의 Playload에 값을 주입하기
==JWT 생성 메서드 작성==
## 에러 핸들링을 활용한 JWT Verify
==JWT 검증 Exception, ErrorCode 작성==
## HTTP Protocol에 대한 로직 마무리하기
==Login, JWT관련 API 작성==
****
# 5. Spring Boot에서 웹소켓 Protocol 활용하기
## HTTP vs WebSocket 이론
### WebSocket
- 트래픽이 빈번한 요청 같은 경우에 많이 사용된다.
==WebSocket에 대한 설명과 이점 STOMP와 같은 프로토콜의 간단한 설명==
## TextSocketHandler를 활용한 Raw Level 코드 작성하기
==말그대로 raw level 소켓 작성법==
## Protocol을 적용하는 WebSocket 및 Long Poiing

****
# 6. 서비스 완성을 위한 부수적인 코드 작업하기

****
# 7. 직접 구동하며 함께 디버깅하기

****
# 8. 더 견고한 프로젝트를 위한 TODO List

****