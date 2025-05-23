# 1. 2탄으로 찾아뵙게 되어서 반갑습니다.
## 어떤 강의를 준비하였는지 알려드리겠습니다.
==1편처럼 쓸개간 다 뺀 강의가 아니라 실무에서 실제로 사용하는 방향으로 강의가 준비되었다==
## 여러분들은 이런 채팅방 관리하는 서버를 만들거에요.
==기존 1편과 다르게 DB, 방생성, 채팅 유지등이 추가되었다.==
## 여러분들은 이런 시스템을 구축 할 예정이에요.
==주키퍼, 카프카, 서버 사용에 시연영상==
****
# 2. 3 Tier Architecture를 구성하면서 시작해봅시다.
## 처음 뵙는분들! 이전 강의에 대한 소스코드를 간단하게 알려드릴게요
==1편의 코드를 리뷰하는데 왜 1편에 없던 기능들이 어디서 추가됫는지 곤란하지만 천천히 따라갈것..==
## 여러개의 서버를 띄우는 강의기 떄문에, 편리성을 위해 Flag를 셋팅할게요.
==Flag command에서 전달할 수 있는 값을 추가==
## 환경변수 매우 중요하죠! 환경변수를 통해서 서버를 실행해볼게요.
## 이러면 Skelton 서버가 구축이 됩니다.
[[Skelton?]]
==최대한 기존 코드를 건드리지 않으면서 network 모듈 리팩토링==
## MySQL에 쿼리를 작성할껀데, ORM은 사용해야할까요?
==ORM을 사용하면 쿼리 추적, 튜닝이 어렵다. DB의 능력이 오르는 느낌보다는 ORM의 기술이 오르는 느낌일꺼라 잘 판단해서 사용하는게 좋다.==
## Paging, Sort 쿼리도 한번 맛을 보면서 알아봐요.
==List형태로 리턴하는 Query작성==
## 실무에서는 이런 구조로 서버가 구성이 되고있어요.
==기본적인 Repository => Service => Controller 같은 구조로 작성 하지만 go style==
## API가 모두 작성이 되었으니, Request에 대한 검증을 진행할게요.
==API 작성==
****
# 3. MySQL을 통해서 Schema를 설계하며, 꿀팁을 배워가세요.
## MySQL에서 테이블 생성은 어떻게하고, 시간에 대한 타입은 뭐가 다를까요?
### ERD 다이어그램
- 실무에서는 [ERD클라우드](https://www.erdcloud.com/) 사이드 프로젝트는 [Draw.io](https://app.diagrams.net/) 추천
### MySQL 시간 타입
- BIGINT -> unix
	- default 불가능
- dateTime -> timezone
	- 실무에서는 dateTime을 쓸것
- timestamp ->
	- 2040년 특정 시간이후 오버플로우 발생 가능
## 강의에서 사용하는 나머지 테이블을 생성해보고, Bool 타입과 TinyInt 타입은 동일할까요?
### bool Type?
- 생성은 bool type `describe table`를 하면 tinyint로 저장되어 있음.
****
# 4. wss, HTTP 프로토콜을 활용하여 서버와 통신하고, DB에 접근해봐요.
## HTTP Protocol을 활용해여 서버에 접근해봐요.
==서버 구동후에 API 테스트를 통해 정상 동작 여부를 확인하고, 발생한 오류에 대해 디버깅을 수행했다.==
## wss Protocol을 활용해서 서버에 접근해봐요.
==chat table insert 작성 및 리팩토링==
## 이제 테스트를 해볼게요. FE 연동을 통해 서버의 디버깅을 진행해봐요.
==프런트 실행후 채팅방, 채팅 기록 확인==
****
# 5. 이제 Kafka를 내 컴퓨터에 한번 설정하고 구동해볼게요.
## 이 강의에서 다룰 zero-downtime-deploy를 위한 아키텍처 구조도를 알려드릴게요
==stateless server일 경우에는 여러개의 server중 하나가 죽었어도 `Controller Server`같은 곳에서 로드밸런싱으로 다른 서버에 보내면 되는건데 stateful server의 경우에는 해당 커넥션이 연결되어 있는 서버가 죽어버리면 이 커넥션을 유지하기 위해 다른 서버에 커넥션을 죽은 서버의 커넥션은 나눠가져야함. 그러다가 또 죽은 서버를 살렸을 경우에도 커넥션을 나눠야하는 일이 발생 그래서 강사는 서버가 죽었어도 바로 커넥션을 나누지 않고 retry를 하는 방식을 추천==
## kafka를 구동하기 전에, 우선 zookeeper를 구동하고 설정해볼게요.
### Zookeeper와 kafka
- kafka는 zookeeper가 존재해야만 kafka가 구동이 될 수 있다.(현재는 미래에는 아님!)
- zookeeper는 카프카에서 발생하는 브로커나 메타데이터를 기본적으로 관리하는 컨트롤 서버 같은 느낌
[Docker Compose zookeeper 참고 블로그](https://devocean.sk.com/blog/techBoardDetail.do?ID=164016)
## zookeeper의 앙상블은 무엇이고, 고가용성은 무엇일까요?
`server.{x}={hostname}:{peerPort}:{leaderPort}`
- x : 원하는 정수 값 순차적일 필요는 없다.
- hostname: 앙상블안의 서버들이 내부 IP 주소
- peerPort: 앙상블안의 서버들이 서로 통신할 때 사용하는 TCP 포트
- leaderPort: 리더를 선출하는데 사용되는 TCP 포트
- clinet는 clientPort로 접근한다. 앙상블끼리는 내부적으로 프라이빗하게 통신하기 때문에 위 정보가 필요하다.
## kafka를 구동시키고, terminal를 통해서 Pub/Sub이 먼지 실습해볼게요.
### topic
- 일종의 키값
`docker compose exec kafka-1 kafka-topics --create --topic test --bootstrap-server kafka-1:9092 --replication 1 --partitions 1`
- 토픽을 생성한다
`docker compose exec kafka-1 kafka-topics --describe --topic test --bootstrap-server kafka-1:9092`
- 생성된 토픽을 확인한다.
==아래 둘은 `docker compose exec kafka-1 bash`상태에서 가능==
`kafka-console-producer --topic test --bootstrap-server kafka-1:9092`
- 토픽을 날린다!
`kafka-console-consumer --topic test --bootstrap-server kafka-1:9092`
- 받는다
### --bootstrap-server
- Kafka 클라이언트가 최초로 연결할 브로커 주소(들)
****
# 6. Kafka도 구동시켰으니, 서버에서 Kafka를 한번 활용해볼게요.
## Server에서 Kafka에 접속해 봐요.
==kafka golang에서 연결 (Failed)==
## zero-downtime-deploy가 중요한데.. MySQL을 통해 관리할게요.
==서버 정보의 IP,Port 정보를 DB에 저장하기, 정확히 어떻게 다루는지는 이후 강의를 봐야할듯==
## Kafka에 Server의 상태에 대한 message를 전송해야하니 서버의 상태를 감시할게요.
==golang의 channel을 이용해서 서버가 죽는 이벤트를 캐치해서 정보를 남길 수 있다.==
## Kafka의 Pub/Sub Modeling을 활용해서, 데이터를 관리해봐요.
==서버 종료시 정상적으로 메시지 발행하는 코드 작성 및 DB 저장 확인 Pub/Sub모델링이긴한데 발행만 한다.. 구독을 따로 하지는 않음 왜냐면 DB저장 로직은 위에서 이미 처리되고 아래에서 메시지를 발행함 그 이후 시나리오는 후에 나오나..?==
****
# 7. 서버의 상태 관리를 위한 Controller Tower 서버를 추가로 만들어볼게요.
## Controller Tower API도 같이 Skelton 구축해 볼게요.
==Controller Tower를 위한 기본적인 세팅 약간의 구조만 다를뿐 기존 서버와 내용은 같다.==
## MySQL을 통해서 서버의 초기 메모리 셋팅 진행할게요.
==serverInfo Table의 값을 불러와서 Map에다가 저장하는 로직까지.==
## avaiable 가능한 서버 리스트를 내려주는 Router를 작업할게요.
==카프카 연동전에 활성화된 서버들을 DB에서 불러와 메모리에 담아 놓는다.==
## 외부 참조를 방지하기 위한 함수와 Kafka의 Subscribe 로직 작업할게요.
==Consumer를 만들고 객체에 대한 캡슐화 작업등도 하고 발행된 메시지에 대한 구독 준비==
## Kafka를 통한 Subscribe 마무리하고, API를 통해 확인해 볼게요.
==사실상 강의 마무리 Kafka 그러니깐 메시지 브로커를 사용하는 프로젝트들의 어쩌면 가장 일반적인 발행 과 구독이 어떻게 이루어 지는지에 대한 강의인거 같다. API들이야 언제든지 바뀔수 있지만 이 구조는 머릿속에 남겨두자==
****
# 8. Go너무 어려운데... Node.Js는 없나요??
## 모두 다룰수는 없으니.. Node.Js에서 Kafka를 활용하는 코드를 작성해 볼게요.
==node로 발행/구독 방법에 대한 코드! 그리고 간단하게 cron을 쓰는법까지==
****
# 9. 강의에 대한 전반적인 소스코드 제공해 드릴게요.

****