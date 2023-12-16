TCP
- 연결(Connection, Session) 개념이 있다.
- 연결은 매우 **논리적(Virtual Circult)**
- 연결의 순서번호는 Byte수 만큼 증가한다
	- 1 : 400 : 2 : 401~
- 연결은 **상태(전이)** 개념을 동반한다.
- 영역은 **Segment** 이라 불린다.
- Client/Server로 구성되어 있다.
	- Server는 연결을 **대기** 하고 있다.
- IP와 Port번호를 알아야 연결이란걸 개념적으로 시도할수 있다.

UDP
- 영역은 **Datagram**이라 불린다.

## TCP 연결 과정 (3-way handshaking)
- 통신되는 단위 **Segment**
	- | IP | TPC | 
		- 이루어져 있고 Payload가 없다.
	- 관리 목적의 Segment가 왔다 갔다한다.
- 랜덤한 숫자의 sequnce number를 던진다.
1. Client.SYN(sequnce number) => Server
2. Server.SYN(sequnce number) + ACK(Client.sequence number + 1) => Client
3. Client.ACK(Server.sequnce number+1) => Server
	1. ACK를 받는순간 *ESTABLEISHED* 가 되었다고 판단한다
- Seq번호과 **정책**정보를 교환한다
	- **MSS(Maxmun Segment Size)** 가 얼마인지 교환한다
	- 낮은쪽으로 MSS를 맞춘다.

## TCP 연결 종료 과정(4-way handshaking)
- 대전제
	- 특별한 이유가 없다면 Client행동이 Active하다.
	- 연결을 요청하는것도 Client 끊을려고 하는것도 Client
1. Client.FIN + ACK => Server
2. Server.ACK => Client
	1. Client - FIN-WAIT1 상태
3. Server.FIN+ACK => Client
	1. Client - **TIME_WAIT**
4. Client.ACK => Server
- Server의 **TIME_WAIT**의 발생은 무언가 문제가 있다는 의미이다.

## TCP Header 형식
- 32bit단위로 표현
- Port 번호는 2^16의 0 과 65535 제외한 숫자
- Sequence number
- Acknowledgment number
- TCP 장애유형
	1. Loss
		1. Segment를 잃어버린 경우
	2. Re-Trans가 오면 자연스럽게 Dup-Ack이 따라오게된다.
	3. Out of Order
		1. Sequence number가 깨진경우
	4. Zero window
		1. 네트워크 속도가 처리속도를 역전되어버린 경우
		2. 프로그램쪽에서 처리해야하는 이슈
- Window Size
	- TCP수준의 여유 Buffer
- Checksum
	- 데이터가 손상된건 없는지 계산할때 사용하는 검사값

UDP Header 형식
- Port
- Length / Checksum
- 혼잡제어를 하지 않는다.
- Client를 배려하지 않음
- UDP가 필요한 이유
	- 예를 들어 게임서버일경우
		- TCP를 이용할경우 **하향평준화**되어버린다.
		- TCP의 혼잡제어 영역을 개발해버리면 된다.
- HTTP3 => UDP