# Open5GCore
- 독일 Fraunhofer FOKUS 연구소에서 개발한 5G 코어 네트워크 구현체로 주로 연구용으로 활용
- 각 네트워크 기능을 개별적으로 실행 할 수 있는 모듈화 구조로 제공 (Docker 컨테이너로 제공)
	- AMF(Access and Mobility Management Function)
	- SMF(Session Management Function)
	- UPM(User Plane Function)
	- UDM(Unified Data Management)
	- PCF(Policy Control Function)
### AMF(Access and Mobility Management Function)
- 단말기가 네트워크에 접속할 때 가장 먼저 접하는 기능
- 접속 요청을 처리하고 인증절차를 시작
- 인증 과정에서 UDM, AUSF와 상호 작용
### AUSF(Authentication Server Function)
- 실제 인증 절차의 핵심
- 단말의 식별자(SUPI/IMSI 등)를 바탕으로 UDM으로부터 필요한 인증 정보(예: 인증 백터)를 받아온다.