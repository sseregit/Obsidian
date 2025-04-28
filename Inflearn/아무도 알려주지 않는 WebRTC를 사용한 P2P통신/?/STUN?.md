# STUN(Session Traversal Utilities for NAT)
- NAT(Network Address Translation)환경에서 피어 간의 직접 연결을 가능하게 하는 핵심 프로토콜
### 역할
- 클라이언트가 자신의 공인 IP 주소와 포트 번호를 알아내도록 도와준다.
- 이정보로 피어 간의 직접 연결을 설정하는데 필요하다.
### 동작 방식
1. Binding Request 전송
	- 클라이언트는 STUN서버에 자신의 공인 IP와 포트를 요청한다.
2. Binding Response 전송
	- STUN 서버는 클라이언트의 요청에 응답하여 공인 IP와 포트 정보를 제공한다.
3. ICE 후보 수집
	- 클라이언트는 수집한 정보를 ICE후보로 등록하고, 이를 시그널링을 통해 상대 피어에게 전달한다.
### NAT 유형과 STUN의 한계
- STUN은 대부분의 NAT 환경에서 효과적이지만 **대칭 NAT(Symmetric NAT)** 에서는 제한적이다. 대칭 NAT는 목적지에 따라 다른 외부 포트를 사용하므로, STUN으로 얻은 정보가 유효하지 않을 수 있다. 이러한 경우 [[TURN?]]서버를 사용하여 중계 연결을 설정해야 한다.