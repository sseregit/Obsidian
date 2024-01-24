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

### 브라우저에 URL을 입력하면 일어나는 일?
1. 브라우저에 URL을 입력한다.
	1. URL
		1. https://www.abc.com
			1. www : host
			2. abc.com : domain
	2. IP주소를 기반으로 접속한다.
		1. HTTP통신에 앞서 TCP/IP통신이 가능해야 한다.
2. IP주소를 알아내는 순서 (Local Machine)
	1. hosts file을 먼저 읽는다.
		1. **보안관리 매우 중요하다!**
	2. DNS Cache를 참고한다.
		1. 질의에 대한 결과를 저장하고 있다.
	3. DNS Query
3. IP를 알아내고 TCP/IP연결을 한다.
	1. HTTP통신 프로토콜은 기본적은로 TCP/IP 베이스로 작동한다.
4. HTTP.request
5. HTTP.response
6. HTML + CSS + img... + JS 를 브라우저에 랜더링한다.
7. Disk에 Web Resource를 cache한다.

- DNS의 작동원리
	- Root DNS
		- 전세계에 13대
		- host를 알려주는곳이 아니다.

## Web server와 HTTP

### HTTP 1.1 vs HTTP/2
- HTTP 1.1
	- 요청과 응답이 한 세트로 이루어져 있다.
	- 직렬적

- HTTP/2
	- 속도가 압도적으로 빠르다.
	- Application (HTTP 2.0)
		- **Binary Framing**
			- 중첩 전송이 가능하게 한다.
		- Session TLS (optional)
		- Transport (TCP)
		- Network (IP)
	- 서버 푸시
	- 헤더 압축
		- 중복요소 압축으로 최적화

- HTTP3
	- Flow-control -> QuIC
	- TLS 필수!
	-  TCP -> UDP

### 네트워크 보안 솔루션 종류별 대응 계층
- Inline
	- Packet Filtering
	- IPS
- Out of path
- SSL 인증서
	- Web Server
	- IPS 에도 설치할수도 있다.
	- LB 에도 설치 될수 있음.

### WAF와 Proxy 구조
- Proxy 구조 (우회)
- Proxy 구조 (서버 보호)
	- WAF