
## JAVA 공부 시작에 앞서...

## C/C++개발자가 바라 본 프로그래밍 언어 JAVA
- JAVA
	- **JVM 기반** 에서 작동하는 OOP언어
	- C/C++의 가장 큰 특징인 **메모리 관리와 책임이슈를 구조적으로 제거**
		- GC
	- OS(혹은 Platform)에 대한 의존성 없음
	- **컴파일러, 인터프리터 특징을 모두 가진다**
		- 인터프리터가 나온다 는 것은 버추얼머신이 나온다는 것과 같다.
	- 문법적으로 C/C++와 매우 유사
- JVM
	- Big endian system으로 구현되어 있다. 80%..?

## Java 공부 02 시작부터 바보짓
- JAVA가 아닌 Java표기가 맞다.
- Short circuit
	- A && B or A || B
		- A가 false 라면 B를 확인할 필요가 없다.
		- A || B는 A가 true일때만 B를 확인하지 않는다.

## Java 공부 03. Java의 언어적 특성에 관한 주관적 견해
- 변수와 자료형
	- C/C++와 거의 동일
	- 자료형
		- 정수 (byte, char, short, int, long)
		- 실수형 (IEEE 754 float, double)
		- 논리형 (boolean)
		- 참조형
	- 객체가 저장된 메모리주소(JVM 범위 한정)를 참조 하는 형식
	- C++의 참조형과 매우 흡사하지만 포인터에 더 가까운 특징이 있다.
		- 깊은복사와 얕은복사 개념이 존재 (hashCode() 메소드)
- 심볼 검색 범위
	- 기본구조는 C/C++와 동일
	- Package에 따른 범위 확장 (C++의 namespace와 유사)
- 문자열 상수 이슈
	- C언어의 문자열 상수는 정적 메모리 영역에 위치
	- **같은 문자열 상수에 대한 포인터는 같은 주소를 가진다.**
	- 이와 동일한 이슈가 Java에도 존재
		- 문자열은 String컨테이너 객체로 관리 되는 것으로 보인다.
- 문자와 정수형
	- 문자는 기본적으로 **Unicode**로 간주
	- byte (8bit), char (16bit)
	- Escape sequence 사용
	- 수치 연산시 Type promotion 발생
		- byte + byte = int
	- 음수의 char형 변환 불가(컴파일 오류)
- Pointer스러운 참조형
	- 참조형에 대한 관계연산(`==`, '!=')은 객체 메모리 주소에 대한 비교
		- Pointer와 동일

## Java 공부 04. 혼란스러운
- C++ 개발자 관점에서 혼란스러운 점
	- 참조형은 포인터가 아닌 것처럼 보이지만 **사실상 포인터**
	- 범위지정연산(::)과 멤버접근연산(.)을 함께 사용
	- 열거형(enum)은 참조형이며 class처럼 개체로 관리(정수 아님)
		- Symbolic 상수
			- 심볼을 부여해 어떠한 문자열로 식별이 된다.
			- 읽기좋은 코드를 위해 Symbolic 상수를 잘사용해야함.
		- 컴파일타임에 많은 에러를 잡아줄수 있는 열거형을 참조형으로 만든것은 큰 장점이다.
	- C++에서는 선언과 정의를 각각 .h와 .cpp로 명확히 구분하지만 Java는 그렇지 않음.
	- Java는 #include 대신 import를 사용하는데 중복이슈가 상대적으로 덜하다.
	- 클래스 이름과 파일명이 대/소문자까지 맞아야 한다.
		- Window는 파일명의 대/소문자에 의미를 두지않는다.
		- Liunx, MacOS...등 파일명의 대/소문자를 구분한다.

## Java 공부 05. 흥미로운 점 - 첫번째
- C++ 개발자 관점에서 흥미로운 점
	- 멤버 데이터 대신 **필드**
	- 참조형 필드의 경우 class 선언 코드에서 new 연산 초기화 가능
	- 생성자에서 다른 생성자 호출 시 this();
	- 부모 클래스의 경우 super();
	- 배열(객체)를 매개변수로 전달
	- **심볼릭 상수** 정의시 final 키워드와 정적 멤버 선언을 조합해 사용
	- 심볼릭 상수라 하더라도 반드시 클래스에 소속되어야 가능
		- 전역 X
	- Package로 namespace와 접근제어 이슈 friend 통합(주관적 견해)
		- 하나의 라이브러리로 인정된다.
	- default 접근 제한자 존재
	- 상속 관련 키워드와 특징
		- extends, abstract
		- instance of 연산자 (C++의 dynamic_cast)
		- 다중 상속 불가
	- 순수 가상 개념이 있으며 좀 더 세분화
		- interface, implements
		- 다중 상속 허용

## Java 공부 06. 흥미로운 점 - 두 번째
- C++ 개발자 관점에서 흥미로운 점
	- 재정의에 대한 표기법 존재
		- @Override annotation
		- Called by framework
	- 중첩 클래스나 로컬 클래스 활용도가 높은 예제가 많음
	- Event -> Handler
		- Event driven 구현된 체계에서 다 적용
		- 특히 GUI
	- toString() 메소드로 클래스 이름을 추출 할수 있음
		- 디버그 모드처럼 보임
	- Runtime 오류
		- JVM -> Dump + Stack
		- 구체적으로 어떤 클래스 어떤 메서드에서 특정된다.
	- 참조의 구현은 결국 포인터
	- hashCode()와 equals() 이슈의 본질은 결국 포인터
	- Native thread와 JVM thread 둘 다 알아야 문제 해결 가능
		- JVM 덤프분석
	- 오픈 소스 라이브러리와 패키지 수준 의존성 관리
	- 의존성에 따른 이슈를 관리해주는 전문 빌드 도구 존재
		- Maven
			- 가져오기만한다
			- pom.xml
		- Gradle
			- 가져오면서 Sciript를 추가할수 있다.

## Java 공부 - 07.JVM 구조
- S/W 구현된 CPU
- Java Byte Code
	- 기계어 -> JVM -> CPU
	- 문자열을 가지고 있다.
		- 상수
		- Class의 이름
		- 메소드의 이름
- Class Loader
	- .class의 의존성 연결을 해준다.
	- Loading
	- Linking
	- Initialization
- Runtime Data Area
	- Memory 영역
		- Method Area
		- Heap Area
			- 객체가 생성되면 사용되는 공간 관리체계가 자동(GC)
			- Young Generation
			- Tenured Generation
			- Permanent Generation
				- Java SE 8 버전부터 PermGen 영역은 제거되었고 Metaspace로 대체 되었다.
				- 리플렉션과 관련이 있다.
				- Class 혹은 Method Code가 저장되는 영역
				- Default로 제한된 크기를 가지고 있다.
		- Metaspace
			- Java 클래스 로더가 현재까지 로드한 Class들의 메타 데이터가 저장되는 공간
			- JVM에 의해 관리는 Heap영역이 아니라 OS레벨에서 관리되는 Native 메모리 영역에 위치
			- Default로 제한된 크기를 가지고 있지 않고, 필요한 만큼 늘어난다.
		- Stack Area
		- PC Register
			- PC
				- Program Counter
		- Native Method Stack
- Execution Engine
	- Interpreter
		- Byte Code를 실제 기계어로 바꾼다.
	- JIT Compiler
		- 코드 캐싱, 성능향상 등...
		- JVM Oracle HotSpot
	- Garbage Collector
- Native Method Interface(JNI)
	- JVM은 C/C++로 개발되었을것이고 그안에 Module 수준에 라이브러리가 있다.
		- .dll 등..
	- 해당 Module들을 인터페이스 형태로 가지고 있다.
	- JVM이 가질수 없는 추가 기능을 가질수 있게 해준다.
	- 보안과 매우 관련있다.

## Java 공부 - 08.클래스 로더
- 클래스로더
	- Loading
	- Linking
	- Initialization
		- 생성자
		- 필드 초기화
- .java 파일을 컴파일해서 얻는 .class를 메모리 로드
- 로드할 클래스가 여럿이면 **Main()** 메서드를 포함하는 클래스를 우선 로드
	- 엔트리 포인트
		- 최초 시작되는 지점
- 로드, 링크, 초기화 단계를 거친다.
### (JVM 내장) 클래스 로더
1. 부트스트랩 클래스 로더
	1. 표준 Java 패키지 로드
	2. rt.jar 파일에 들어있는 핵심 라이브러리
2. 확장 클래스 로더
	1. $JAVA_HOME/jre/lib/ext
	2. 확장 라이브러리 클래스 로드
3. (응용 프로그램) 클래스 로더
	1. (-classpath, -cp) 클래스 경로에 있는 클래스 로드
	2. 일반적으로 개발자가 작성한 코드를 포함하는 클래스
	3. 로더가 클래스 이름을 찾지 못할 경우 NoClassDefFoundError, ClassNotFoundException 에어 발생

- 클래스 링크
	- Runtime Link
	- 클래스 로드후 링크 절차를 수행하며 클래스간 의존관계를 분석하고 함께링크
		- DLL 라이브러리 로딩할때와 방식이 같음
	- 확인
		- .class 파일자체에 대한 구조 정합성 검증
		- 실패 시 VerifyException 에러 발생
	- 준비
		- 정적 필드에 메모리를 할당하고 기본값으로 초기화
		- 생성자 호출전이며 일단 0 초기화

- 클래스 초기화
	- 클래스 생성자 호출
	- 정적 필드에 0이 아닌 초깃값을 기술할 경우 실제 값으로 초기화
	- 멀티스레드 환경을 고려하지 않을 경우 클래스 초기화 중 오류발생 가능
		- 생성자 -> 함수(메서드)
		- **생성자에서 멀티스레드에 관련된 동기화와 관련된 코드를 넣으면 안된다.**

## Java 공부 - 09.JVM Runtime data area
- JVM Runtime data area
	- Virtual 에서 Native가 나오면 OS수준 이라 생각하면 된다.
	- Method Area
		- **상수 풀**
		- 필드
		- 메서드 코드 등이 저장되는 영역
	- Heap Area
		- 클래스 인스턴스들이 저장되는 런타임 데이터 영역으로 GC가 관리
		- new 연산으로 생성된 모든 클래스 인스턴스가 저장되는 영역
		- 멀티스레드 환경에서 Heap영역은 모든 스레드가 공유 (동기화 필수)
	- Stack Area
		- 각 스레드마다. 별도의 스택을 가진다.
		- 메서드 호출 시 스택 프레임이 증가하며 각 반환시 프레임 자동 소멸
		- 지역변수, **피연산자**, 스택 프레임 데이터등 세 가지 요소로 구성
			- JVM = Stack Based Machine
		- 피연산자와 프레임
			- 스택기반 머신 형태로 작동하도록 구성
			- 연산의 중간결과도 스택에 저장
			- 스택의 최대 크기는 컴파일 타임에 결정
				- 자바 컴파일러가 bytecode를 변환할때 스택의 크기가 결정됨
			- 메서드에 대한 모든 심볼정보 및 예외처리 관련 catch 블록 정보 등은 프레임 데이터 영역 사용
	- PC(Program Counter) Register
		- 일반 CPU(EIP register)처럼 Program Counter를 가지며 같은 역할 수행
			- EIP register가 보통 문맥
		- 스레드 마다 별도 문맥을 가질 수 있도록 개별 PC register를 가진다.
	- Native Method Stack
		- Native == OS와 관련된 영역
		- C/C++같은 Native 언어로 개발된 메서드를 지원하기 위한 스택
		- 스레드 마다 별도로 제공
		- JNI(Java Native Interface)
			- 안드로이드에서는 굉장히 신중히 다루는 영역이다.

## Java 공부 - 10. JVM heap 영역
- Java SE 8 버전 부터는 PermGen 영역이 제거되고 Metaspace로 대체 되었다.
- Permanent Generation
	- Permanet Generation은 Class 혹은 Method Code가 저장되는 영역
	- PermGen은 Heap 영역에 속함
	- **Default로 제한도니 크기를 가지고 있다.**
- Metaspace
	- Metaspace는 Java 클래스 로더가 현재까지 로드한 Class들의 메타데이터가 저장되는 공간
	- JVM에 의해 관리되는 Heap 영역이 아니라 OS 레벨에서 관리되는 Native 메모리 영역에 위치
	- Default로 제한된 크기를 가지고 있지 않으며, 필요한 만큼 늘어난다.
- JVM heap 영역
	- Metaspace (Java 8)
		- 로드되는 클래스, 메소드 등에 관한 메타 정보 저장 (자동확장 기능)
		- **Java heap이 아닌 Native 메모리 영역 사용**
		- 리플랙션 클래스 로드 시 사용 (Spring)
	- Permanent generation (Java 7)
		- 로드되는 클래스, 메소드 등에 관한 메타 정보 저장(**고정 크기**)
		- 리플렉션 클래스 로드 시 사용 (Spring)
	- New (Young generation)
		- 새로 생성한 개체가 사용하는 영역
		- **Minor GC** 대상 영역
		- Eden, From, To 요소로 구성
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
		- Mark & Compact 알고리즘
		- 정적인 정보를 많이 사용하면 Old를 사용하게 된다.