# 1. 강의 소개
## 강의 소개
==왜 해당 강의를 만들었는지==
****
# 2. RPC는 무엇인고, GRPC는 또 무엇일까..?
## RPC란 무엇이고, 어떤 구조에서 사용을 해야할까..?
### RPC가 유용한 상황
- gateway같이 외부서버와의 연결 그리고 내부 서버와의 연결이 자주 일어나는 서버일 경우
==RPC가 무엇이고..? 그냥 검색한거고 유용한 상황은 gateway처럼 내외부와의 많은 통신이 일어나는 서버일 경우==
## GRPC란 무엇일까..?
### GRPC
- google에서 개발한 RPC 프레임워크
- GRPC를 구현하는데 있어 Proto라는 자기들만의 언어가 있다.
==grpc.io를 그냥 보면서 Proto라는 언어를 쓴다 이런 느낌...==
****
# 3. 실무에서 사용하고, 칭찬받는 서버 구조 작성하기
## 해당 강의에서 사용하는 패키지 종류 입니다.
==사용하는 package==
## 기본적인 구조 관리하기
==구조마다의 역할 설명==
## Flag를 통해 확장성있게 환경변수 관리하기
==flag를 사용하기==
## 다양한 객체를 관리하는 관리성 객체 생성하기
==사용할 객체들 초기화 하기==
## 오픈소스를 활용하여 서버 구동하기
==gin 을 활용해서 서버 실행하기==
****
# 4. RPC 서버 구동 및 Google의 언어인 Proto작성하기
## JWT와 Paseto 비교 및 Paseto 활용하기
[[Paseto?]]
==활용보다는 Paseto를 사용하기 위한 struct와 코드 작성==
## Google의 GRPC언어인 Proto 작성하기
==proto 파일 작성 message는 기본적인 string, int64와 같은 필드들을 가질 수도 있고 message를 필드로도 가질 수 있다 1, 2, 3같이 인덱스같은 것을 지정하는데 중복은 불가능 service는 함수들을 선언==
## Proto Build하기 위한 명령어 알아보기
==protoc를 사용하기 위해서는 protobuf를 사용해야 한다. protoc를 활용한 커맨드로 go파일을 자동으로 생성할 수 있다.==
## RPC통신을 위한 GRPC Client 생성하기
==GRPCClient struct 생성==
## RPC 통신을 위한 GRPC Client 연결하기
==말그대로 grpc와 연결하기 위한 코드 작성==
## PasetoToken에 대한 비지니스 로직 구현하기
==paseto.V2를 활용한 Encrypt, Decrypt==
## GRPC Client의 요청을 처리할 수 있는 백그라운드 Server 구동하기
==GRPC서버를 다른 스레드에서 구동하게끔 go func{}() 사용==
## GRPC Server의 interface 구현을 위한 메서드 추가하기
==GRPC Server의 AuthServiceServe interface 구현==
****
# 5. RPC 서버와 HTTP 서버 연동하기
## HTTP 라우터와 GRPC 서버 연결하기
==GRPC서버를 실행하기 위한 구조 변경==
## PasetoToken 검증을 위한 미들웨어 작성하기
****
# 6. 프로젝트 디버깅 및 강의 마무리

****
# 7. 소스코드를 제공합니다!

****