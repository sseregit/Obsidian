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