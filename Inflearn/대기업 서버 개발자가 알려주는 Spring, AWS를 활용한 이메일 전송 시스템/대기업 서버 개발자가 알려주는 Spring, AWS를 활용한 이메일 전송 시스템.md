# 1. 강의 소개
## 강의소개
==해당 강의의 목표는 서비스 플랫폼에서 이메일을 다루는 법 패스워드, 인증등 어떤식으로 이메일을 활용할 수 있는지에 대한 강의가 될 것이다.==
****
# 2. Spring Initializer
## Spring 시작하기, @SpringBootApplication
==spring.start.io 사용과 @SpringBootApplication의 대한 설명 [[2장 질문]]의 1번 문제의 답변을 참고하면 된다 ==
## Install Dependencies
==사용할 Dependencies에 대한 설명 대략적으로 jpa, web, gson, lombok, aws, openapi...==
****
# 3. Spring Common
## ErrorCode 정규화
==ErrorCode 관리를 위한 클래스 작성==
## CustomException
==ErrorCode를 받아 사용하는 CustomException 작성==
## Constraints For Singleton
==자바에서 상수값을 다루는법과 해당 클래스를 private 생성자로 작성해 싱글톤을 만드는 것==
## Validator
==Email 정규표현식을 활용한 Validation 작성==

****
# 4. Spring Config
## AWS SES Client
==@Configuration과 @Value를 활용한 SesClient 빈 등록하기.==
## Bean For TransactionManager Annotation
### `@EnableTransactionManagement`
- 스프링의 선언적 트랜잭션 기능을 활성화하는 애노테이션
- 기본적으로 자동 설정이 되는 애노테이션 starter-jdbc, starter-jpa등등..을 사용할 시
==보통은 application.yml 이나 properties를 활용해서 자동 빈 등록으로 DataSource나 TransactionManager를 쓰는데 직접 등록했다.==

****
# 5. Spring Security
## [[OTP?]] Generate
==OTP에서 사용할 QRCode를 만드는 오픈API에 값이 넣어주는 함수 작성==

****
# 6. Spring Controller
## Swagger & Router
==OTP 전송을 위한 Controller 작성 및 openapi annotaion 활용==
## Req/Res Model
==아주 아주 아주 단순한 요청 모델과 응답 모델 작성==
## Service Logic
@GetMapping에서 @RequestBody의 사용은 좋은 선택이 아니다.
==아주 아주 아주 단순한 Serice 작성 로직도 존재하지 않음 이후에 작성 예정==
## AWS SES Service
==SesClient를 활용해서 메일을 보내는 Service에 함수 작성==

****
# 7. Spring Repository
## JPA Entity
==아주 아주 아주 단순한 User Entity 작성==
## Repository & TMI
==아주 아주 아주 단순한 JPARepository 작성 그리고 JPA를 사용할 때 설계에 대한 완성도가 중요하다는 말을 했는데 잘 이해가 안됨..?==

****
# 8. AWS
## SES 전송을 위한 Service 작성
==이메일 전송을 위한 서비스 로직 작성==
## SES Template JSON
==SES에서 사용할 Template JSON 파일 작성==
## SES의 자격증명 및 SandBox 제약
****
# 9. Debug

****