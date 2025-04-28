# TURN(Traversal Using Relays around NAT)
- 피어 간 직접 연결이 불가능할 때, 미디어 트래픽을 중계하여 통신을 가능하게 하는 프로토콜이다.
### 역할
- STUN과 달리, 클라이언트가 TURN 서버를 통해 중계 주소를 할당받아, 모든 미디어 트래픽을 해당 서버를 통해 전달한다. 이는 대칭 NAT(Symmetric NAT)나 엄격한 방화벽 환경에서 유일한 연결 수단이 될 수 있다.