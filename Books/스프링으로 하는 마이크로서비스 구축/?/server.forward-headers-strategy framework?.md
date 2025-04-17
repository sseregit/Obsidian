# server.forward-headers-strategy: framework
- X-Forwarded-* 헤더를 Spring이 어떻게 처리할지를 지정하는 설정

### 설정값 종류
#### nono (default)
- 어떤 프록시 헤더도 신경 쓰지 않는다. (로컬 개발등에 적절)
#### native
- WAS의 내부 기능(native support)를 사용해 처리
#### framework
- Spring Web 자체의 처리 로직을 사용해 X-Forwarded-* 헤더를 반영한다.

### 적용 대상 헤더
#### X-Forwarded-For
- 원래의 클라이언트 IP
#### X-Forwarded-Host
- 원래의 요청 호스트
#### X-Forwarded-Port
- 원래의 요청 포트
#### X-Forwarded-Proto
- http or https