## 도서관리 애플리케이션 리팩토링 준비하기 목표

## 테스트코드란 무엇인가?! 그리고 왜 필요한가?

### 테스트코드란 무엇인가?!

### 테스트 코드는 왜 필요한가?!
1. 개발 과정에서 문제를 미리 발견할 수 있다.
2. 기능 추가와 리팩토링을 안심하고 할 수 있다.
3. 빠른 시간 내 코드의 동작 방식과 결과를 확인할 수 있다.
4. 좋은 테스트 코드를 작성하려 하다보면, 자연스럽게 좋은 코드가 만들어 진다.
5. 잘 작성한 테스트는 문서 역할을 한다.

## 코틀린 코드 작성 준비하기

## 사칙연산 계산기에 대해 테스트 코드 작성하기

## 사칙연산 계산기의 나눗셈 테스트 작성

## Junit5 사용법과 테스트 코드 리팩토링

### Junit5에서 사용되는 5가지 어노테이션
1. @Test
2. @BeforeEach
3. @AfterEach
4. @BeforeAll
5. @AfterAll

### 단언문

## Junit5으로 Spring Boot 테스트하기

### 각 계층을 테스트
Domain
- 클래스를 테스트하는 것과 동일
Service & Repository
- 스프링 빈을 사용하는 테스트 방법 사용 (@SpringBootTest)
- 데이터 위주 검증
Controller
- 스프링 빈을 사용하는 테스트 방법 사용 (@SpringBootTest)
- 응답 받은 JSON을 비롯한 HTTP 위주의 검증

## 유저 관련 기능 테스트 작성하기

## 책 관련 기능 테스트 작성하기

## 테스트 작성 끝! 다음으로!

## Kotlin 리팩토링 계획 세우기

### 목표
1. Java to Kotlin
2. Kotlin + JPA
3. Kotlin + Spring
4. Java to Kotlin으로 리팩토링 해야하는 상황에 대한 경험을 쌓는다.

Domain 부터 시작 POJO, JPA Entity
Repository - Spring Bean에 의존 X
Service - Spring Bean에 의존성 O, 비즈니스 로직
Controller - Spring Bean, 의존성 O, DTO의 경우 그 숫자가 많음

## 도메인 계층을 Kotlin으로 변경하기 - Book.java