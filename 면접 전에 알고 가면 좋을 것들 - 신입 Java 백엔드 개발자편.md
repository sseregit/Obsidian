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

### SSL 인증서
- 접속하는 대상이 **공증**하는것에 쓰인다.
- PKI
	- Public Key infrastructure
	- 평문 <-> 암호문
	- 비대칭키
		- 대표적인 알고리즘 RSA
	- X.509이 인증서 파일
	- 인증 체계
		- CA
		- RA
		- PAA
		- PCA
- Session key
	- Client가 생성한 Session key로 Http를 암호화 시킨다.
- SSL 인증서란?
	- Public Key이고 해당 Key를 CA로 부터 발급을 받아 위/변조가 되지 않은것을 보장하기위해 디지털 서명이 포함되어 있다.
	- HTTP 암호화는 Client가 생성한 Session key로 한다.

### JVM 기본구조
- Stack + 자동
- **Heap Area**
	- 메모리를 사용할때 가장 많은 영역을 차지하는 영역.
	- Instance는 Heap에 저장되고 메모리를 관리 하지않고 관리는 **G.C**가 관리르 해준다.

### CG 원리

- Java 8 JVM heap 영역
	- Total Size가 정해져 있는 유한자원
- GC -> 속도이슈가 생긴다.
- Young Generation
- Old Generation
	- 사리지지 않은 객체가 늘면서 이순간 많이 소모 하게 된다.
- Metaspace
- JVM heap 영역
	- Metaspace (Java 8)
		- 로드되는 클래스, 메소드 등에 관한 메타 정보 저장(자동확장 기능)
		- **Java heap이 아닌 Native 메모리 영역사용**
		- 리플렉션 클래스 로드 시 사용 (Spring)
		- 메모리가 더 커져야 할 경우 생긴다.
			- 얼마나 메모리를 소모하는 계산해야한다.
				- 계산의 기준
					- Request
					- 단위시간 -> TPS
	- New (Young generation)
		- 새로 생성한 개체가 사용하는 영역
		- Minor GC 대상 영역
		- Eden, From, To 요소로 구성
			- 인스턴스 최초 생성시 Eden에 생성
			- 그후 From 이나 To로 이동
			- 남겨야할 것이 남겨지면 To로 옮겨놓고
			- From을 Flush해서 싹 비워버린다.
			- 그후엔 다시 To를 From으로 두는식으로 반복
		- Eden
			- 객체 생성 직후 저장되는 영역
			- Minor GC 발생 시 Survivor 영역으로 이동
			- Copy & Scavenge 알고리즘
		- Survivor 0, 1
			- Minor GC 발생 시 Eden, SO에서 살아남은 객체는 S1로 이동
			- S1에서 살아남은 객체는 Old 영역으로 이동
			- age bit 사용 (참조계수)
	- Old (Old generation)
		- Young generation 영역에서 소멸하지 않고 남은 개체들이 사용하는 영역
		- **Full GC** 발생 시 개체 회수
			- Full GC발생시 **지연**이 발생했다고 보면된다.
		- Mark & Compact 알고리즘
- JVM Garbage collector
	- Heap 영역에서 참조되지 않는 개체를 수집 및 제거해 메모리 회수
	- Minor/Major(Full) GC
	- GC수행 시 프로그램 일시정지
		- JVM에 따라 다를수 있다.
		- stop-the world
	- GC 속도
		- Minor GC가 보통 1초 이내 완료
		- Full GC는 수초 이상 진행되기도 하며 이 지연 때문에 DB 연결이 끊기는 등 운영문제가 발생할 수 있음
	- GC Roots (규칙)
		- Stack 데이터
		- 메서드 static 데이터
			- static 데이터는 Old까지 갈 확률이 높음.
		- JNI로 만들어진 데이터

### GC 종류
- Minor와 Full 장애로 이어지고 그걸 해결할 능력이 있나 없나
- Serial GC
	- 단일 스레드 환경 및 소규모 응용 프로그램을 위한 간단한 GC
- Parallel GC
	- JVM 기본 옵션(Java 8 기본)
	- 멀티스레드 기반(개수 지정 가능)으로 작동해 효율을 높임
	- Low-pause(응용 프로그램 중단 최소화)
	- Throughput(Mark & Compact알고리즘을 기반으로 신속성 최대화5)

### APM과 NPM
- Application Performance Management
	- 제니퍼(유료), Scouter(무료 오픈소스)
- Network Performance Management

### Apache JMeter
- 웹 서비스 시스템 성능 계측을 위한 부하 생성 동구
- Java 기본 오픈소스
- HTTP, HTTPS 모두 지원
- CLI 지원
- 외부 플러그인 지원

부하테스트!!! 부하스테스트!!! 부하테스트!!! 는 엄청난 도움이 될것이다.

### 인덱싱을  하는 이유는 무엇일까?
- Database -> 자료 구조
- 인덱싱을 하는 이유
	- 테이블에 대한 검색 속도를 높이기 위해 생성하며 컬럼에 적용
	- 주로 B-Tree 혹은 B+Tree 자료구조로 구현되는 것이 일반적
		- B-Tree
			- 인덱스 노드라고 부른다. 정보가 같이 남아있어 B+Tree보다 약간더 빠름
			- 추가 삭제하기가 용이하다
		- B+Tree
			- 데이터가 수정 삭제가 잘 안되고 쌓이기만 할경우 B+Tree로 인덱스를 걸어주는것이 좋다.
			- 인덱스 검색속도는 가장빠름
	- 대규모 테이블에 대해 적용하며 삽입, 수정, 삭제가 자주 발생하지 않는 경우에 활용
		- 1억건 > 대규모 > 10만건 정도..?
	- 인덱스가 있을 경우 검색속도 증가
	- 테이블에 없는 정보 검색 시 빠른 판단이 가능
- 인덱싱에 따른 오버헤드
	- 인덱스를 위한 메모리 추가 소모
	- 데이터 삭제 시 인덱스까지 수정해야 하는 오버헤드

### 트랜잭션에 대해 물어본다면...
- 질의 수행 시 일련의 작업이 모두 수행되거나 하나라도 실패 시 모두 취소될 수 있는 작업의 논리적 단위
- 모든 절차에 대해 원자성이 보장되어야 한다.
- TPS
- ACID 특성
	- 원자성
	- 일관성
	- 격리성
	- 지속성
- 동시성 관련 이슈
	- 커밋 완료 전 Read (Dirty read)
	- 커밋 완료 전 Overwrite
	- Read 중 데이터가 변경되는 경우
	- 변경한 데이터 유실 (Lost update)
- 트랜잭션 isolation level
	- READ UNCOMMITED
	- READ-COMMITED
	- REPEATABLE READ
		- 트랜잭션 동안 데이터를 읽게 한다
		- 특정 버전에 해당하는 데이터를 읽는다.
	- SERIALIZABLE
		- 처리 속도가 늦어짐