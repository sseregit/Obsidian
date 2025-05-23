# Model Drive Development
[Toss 서버 개발자로 이직하려는 분들께 드리는 조언](https://www.youtube.com/watch?v=zqgytPhmyes&t=1s)

## 기준영상의 표

| 구분          | 구조적 방법론                | 객체지향방법론                      | CBD                 | MDD                        |
| ----------- | ---------------------- | ---------------------------- | ------------------- | -------------------------- |
| 특징          | 프로그램 로직 중심<br>프로그램 모듈화 | 객체에 데이터와 로직 통합<br>상속에 의한 재사용 | 컴포넌트에 인터페이스 추가      | 메타 모델을 이용한 개발 자동화          |
| 주요<br>지원 언어 | COBOL, C, PAS, CAL     | C++, Java, C#                | 모델링 언어,<br>개발언어는 무관 | 모델링 언어, 개발언어는 무관           |
| 출현시기        | 1970년대                 | 1990년대                       | 2000년대              | 2000년대                     |
| 핵심요소        | 프로세스                   | 객체                           | 컴포넌트                | 모델                         |
| 목적          | 비즈니스 프로세스 자동화          | 실제 현실세계를 반영한 유연한 시스템         | 컴포넌트 개발 및<br>재사용    | 개발 플랫폼에 자유로운 자동화된 소프트웨어 개발 |
## 해당 기준으로 DDD와 EDA가 궁금해 GPT를 이용한 표

| **구분**          | **구조적 방법론**      | **객체지향 방법론**      | **CBD (컴포넌트 기반 개발)**         | **MDD (모델 기반 개발)**        | **DDD (도메인 주도 설계)**       | **EDA (이벤트 기반 아키텍처)**        |
| --------------- | ---------------- | ----------------- | ---------------------------- | ------------------------- | ------------------------- | ---------------------------- |
| **출현 시기**       | 1970년대           | 1990년대            | 2000년대 초                     | 2000년대 중반                 | 2004년 (Eric Evans 저서)     | 2000년대 초 (Pub/Sub 등장)        |
| **현재 트렌드**      | 유지보수 부담으로 거의 사장됨 | 여전히 기본 개념으로 활용됨   | 프론트엔드/백엔드 컴포넌트화에 재조명         | 로우코드/노코드 도구와 함께 부활 중      | MSA, 클린 아키텍처와 함께 재유행 중    | 대형 분산 시스템, 서버리스에서 폭넓게 사용     |
| **핵심 요소**       | 프로세스             | 객체                | 인터페이스 + 컴포넌트 조립              | 메타모델, 자동화                 | 도메인 모델, 유비쿼터스 언어          | 이벤트, 이벤트 브로커, 핸들러            |
| **특징**          | 절차 중심, 정형화된 흐름   | 객체 단위로 로직과 데이터 통합 | 조립 가능한 단위로 구성                | 모델 기반으로 코드 자동 생성          | 복잡한 도메인을 중심으로 설계          | 이벤트 기반 비동기 메시징 구조            |
| **목적**          | 비즈니스 절차 자동화      | 현실 반영 + 유연성       | 재사용성과 유지보수성 향상               | 생산성 증가 + 반복 작업 자동화        | 비즈니스 가치와 복잡성 해결 중심        | 느슨한 결합, 반응성 향상               |
| **대표 사용 언어/도구** | C, COBOL, Pascal | Java, C++, C#     | JS(React), Java(Spring), etc | UML, Enterprise Architect | Java, Kotlin, Spring Boot | Kafka, RabbitMQ, AWS SNS/SQS |
## GPT추천 함께 알아야할 표

| **구분**          | **Hexagonal Architecture**  | **Serverless Architecture** | **Clean Architecture**            | **TDD/BDD**                    |
| --------------- | --------------------------- | --------------------------- | --------------------------------- | ------------------------------ |
| **출현 시기**       | 2005년경 (Alistair Cockburn)  | 2014년경 (AWS Lambda 등)       | 2012년경 (Uncle Bob 확산)             | 2000년대 초반 (Agile과 함께 확산)       |
| **현재 트렌드**      | DDD/클린 아키텍처와 함께 급부상         | 이벤트 중심 시스템에서 급성장            | 다양한 산업군에서 설계 지침으로 사용              | 테스트 자동화, QA 문화의 핵심 축           |
| **핵심 요소**       | 포트(Port), 어댑터(Adapter)      | 함수(Function), 이벤트, 트리거      | 계층적 분리, 의존성 역전, Use Case 중심       | Given-When-Then, 단위 테스트        |
| **특징**          | 외부와 내부 완전 분리, 유연한 구조화       | 인프라 관리 없이 코드 중심 개발          | 기술 무관한 도메인 중심 구조 설계               | 요구사항 기반 개발, 품질 내재화             |
| **목적**          | 변경에 유연한 구조, 테스트 용이성         | 자원 최적화, 운영 비용 최소화           | 코드 유지보수성과 변경 용이성 향상               | 초기 품질 확보 및 빠른 피드백 루프           |
| **대표 사용 기술/도구** | Spring, NestJS, Micronaut 등 | AWS Lambda, Azure Functions | Spring, .NET Core, CleanArch Libs | JUnit, Jest, Cucumber, Mocha 등 |