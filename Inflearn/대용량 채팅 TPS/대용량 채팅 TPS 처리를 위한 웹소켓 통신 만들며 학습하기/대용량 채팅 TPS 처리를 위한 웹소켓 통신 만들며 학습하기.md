# 1. 강의 소개 및 강의 목표 설명
## 강의 소개 및 최종 결과물에 대한 정보를 제공합니다.
==강의의 목표 및 최종 결과물==
## Server에 대한 소스코드 입니다.
==강의 소스==
****
# 2. websockets 통신이란 무엇일까?
## webSocket이 동작하는 방식에 대해 알아봅시다.
[draw.io](draw.io)
- 다이어그램 만드는데 사용할 수 있다.
[[event driven?]]
==일반적인 webSocket이 동작하는 방식==
## websockets 사용시 주의할 점
==커넥션이 유지되는 만큼 변화(원하는 서버와의 커넥션)에 대응하지 못할 수 있다.==
****
# 3. 채팅 관리를 위한 websockets 서버 만들기
## 기본 실행 함수 관리하기
==init()은 main()함수 시작하기전에 실행한다.==
## Framework를 통해 서버 실행하기
==gin Framework로 서버 실행하기==
## 미들웨어, Cors 설정하기
==logger, Recovery와 Cors 설정==
## 채팅방 구성을 위한 기본 객체 설정하기
==객체 생성==
## HTTP 통신을 websockets 통신으로 포팅하기
==HTTP 통신을 websockets 통신으로 포팅하는 Upgrader사용==
## websockets통신에 대한 연결 및 끊김 처리 로직 작성하기
==생성한 Room에 Join과 defer를 이용한 Leave `<-` ==
## socket 이벤트 감지를 위한 채널 처리 함수 작성하기
==Golang의 chan type을 다루는 select {}를 활용해 join, leave, msg forward 작성==
## socket message 이벤트 처리를 위한 client 함수 작성하기
==Goroutine을 활용한 msg 읽고 쓰기==
## 작성된 코드를 통해 프로토타입 구동 확인하기
==갑자기 뜬금없이 프론트를 열어서 소켓이 잘되는지 확인한다... 다다음 강의에서 프런트 내용이 나옴==
## 서버 로깅을 통해 이벤트 처리 순서 확인하기
==로그를 위한 Read, Write에 log 추가==
## 동시성 처리에 대한 에러 핸들링 추가하기

****
# 4. React 코드에 대한 가이드라인
## 프론트 탬플릿 파일입니다.
==파일 제공==
## 프론트(React) 에 대해서 간단한 설명 드리는 영상입니다.
==프론트에 대해 자세하진 않지만 어떤식으로 구성이 되어있다 정도의 강의.==
****
# 5. Node.Js로 똑같은 websockets 서버를 구성해보자
## 서버의 기본 구조 작성하기
==JS에서의 기본 구조 잡기==
## 판교 개발자의 bolierplate logger
==판교 개발자..? 라기 보단 그냥 winston과 winston-daily를 활용한 format사용==
## Class를 통한 소켓 통신 제어하기
==Room.go을 Room.js으로 구현==
## winston을 통한 로깅 설정 및 서버 시작하기
==log추가 및 서버 시작==
## Socket Connection 연결하기
==서버 실행후 Front에서 접근처리 확인하기==
## Socket message 처리 함수 작성 및 유저 데이터 추출하기
==쿠키에 저장된 유저 정보 가져오기 및 메시지 처리==
## 프로토타입 구동 확인하기
==마무리!==
****

# 6. 강의 마무리
## 들어주셔서 감사합니다. 편하게 질문주세요.
****
