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

****
# 4. JWT에 대한 모든것

****
# 5. Spring Boot에서 웹소켓 Protocol 활용하기

****
# 6. 서비스 완성을 위한 부수적인 코드 작업하기

****
# 7. 직접 구동하며 함께 디버깅하기

****
# 8. 더 견고한 프로젝트를 위한 TODO List

****