# 1. 강의 소개
## 강의 소개
### Gateway가 활용되는 곳
- 단일 진입을 위한 API 패턴을 활용할 때
	- 단일 지점이기 때문에 단일 실패 지점으로서 동작할 수 있다는 단점!
==Gateway, circuit breaker를 다루어 본다!==
## 사용하는 package
==사용하게 될 go package==
****
# 2. Diagram 및 환경 변수 구성하기
## Module 구성도 Diagram
==해당 강의의 목표가 되는 구성도 작성==
## 가장 기본적인 환경 변수를 위한 코드 작업
==시작전 struct잡아 두기==
****
# 3. Router 환경 변수 및 Kafka 환경 변수 구성하기
## client 호출을 위한 Router yaml 객체 작성하기
==Http 통신을 위한 struct 세팅==
## Message 전송을 위한 Producer yaml struct 작성하기
==Kafka를 위한 Config struct 작성==
****
# 4. Kafka Producer 및 Http Client 작성하기
## Kafka Producer 구현하기
==Kafka Producer를 위한 코드 작성==
## builder pattern 및 restry를 활용한 Http Client 커스터마이징
==client를 사용하는것과 외부 패키지를 사용하는 것에 있어서 커스텀하게 컨트롤 할수 있는 방법 제시==
## 함수 추상화를 활용한 Client 리시버 작성하기
==Http Client를 범용적으로 사용할수 있는 코드 작성==
****
# 5. Routing engin 및 Routing 처리하기
## Routing engine 구현하기
==fiber engine을 활용해 Root역할을하는 Router 작성==
## Module에서의 Routing 처리 1
==Router를 DELETE, POST, PUT에 대한 handler 작성==
## Module에서의 Routing 처리 2
==Router Get에 대한 handler 작성==
****
# 6. Module 구동 및 테스트 진행하기
## 구동을 위한 dependency Injection
==go.uber.org/fx 를 활용한 Module 생성 Producer, HttpClient, Router==
## lifecycle 관리하기

****
# 7. Kafka를 활용한 Api Trace하기

****
# 8. Cricuit breaker

****