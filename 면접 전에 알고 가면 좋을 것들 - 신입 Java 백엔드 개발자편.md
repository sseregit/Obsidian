**Wireshark**
- Network 분석 S/W

HTTP method
- PUT과 DELETE
	- 보안상의 이슈에 대해 생각할수 있어야한다.

Web client -> Web servce -> WAS -> Database
- 흐름과 구조
- Web client
	- Front 영역
- 그외의 영역
	- Back end 영역

## 웹 서비스 구조

- Internet의 핵심적 기술 2가지
	- HTTP
		- **Stateless**
	- HTML
		- 문서

- JavaScript
	- 실행되는 시점 **Client**이다.
	- 저장은 Server에 되어있다.

- 웹서비스에서 Front Side/ Client를 이루고 있는 3요소
	1. 구문분석 가능한 HTML Parser
	2. Parsing 결과에 따른 랜더링
	3. 랜더링된 결과에 JS까지 구동가능한 엔진

- 단반향 -> **양방향 상호작용**
	- 상호작용에 따른 상태 -> 전이 -> 기억
	- 기억
		- Server => Database
		- Client => Cookie
			- key=value

- **사용자 입력**
	- 신뢰 하면 안됨 절대
	- 반드시 검증해야 한다.

- APM
	- 응답 시간이나 JVM을 관리함
	- 프로그램
		- 제니퍼
		- Scouter
		- Xlog

- 보안요소 3가지
	- IPS
		- 가장 기초적인 수준 1차
	- SSL
	- WAF
		- 2차
	- 1차와 2차 보안을 최소한 갖춰야지만 ISMSP 인증을 받을수 있다.

- Native Code
	- CPU 와 OS에 작정하고 의존적일때
	- C와 C++

- Java
	- Managed code
	- Machine이아닌 다른곳에 의존적

- Machine과 VM
	- Big endian system
	- JVM
		- OS + MEM + CPU 관련된 모은것을 한곳에 다 가지고 있는 형태

- 비동기 입출력과 Multi threading은 서로 따로 생각해야한다.

- 