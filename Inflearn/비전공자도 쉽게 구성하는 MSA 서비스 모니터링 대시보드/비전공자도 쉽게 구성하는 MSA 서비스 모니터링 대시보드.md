# 1. 강의 소개와 이런것을 만들어 보실 예정입니다.
## 강의 소개
==강의의 목표 MSA, MA 아키텍처에 대한 설명과 서비스에 어울리는 아키텍처에 대한 선택 방향성등을 제시해준다. OpenTracing 관련한 내용도 강의에 포함한다.==
## HotRod를 활용한 구현체 확인하기
==간단한 UI들을 통해 OpenTracing에 대한 예제 확인==
## Docker &amp; VM 이렇게 쉽게 알려드립니다.
==매우매우 기본적인 VM과 Docker container에 대한 이야기==
****
# 2. 📖 MSA와 MA에 따른 차이점과 Trade Off (PDF 이론)
## 강의에서 사용하는 자료 입니다.
==자료 다운로드==
## MSA와 MA의 대표적인 차이점 알아보기
==Monolithic -> N-Tier -> Microservices 에 대한 흐름 정의를 살펴보았다.==
## 그림으로 알아보는 MSA에서의 분산추적
==그림으로 살펴본 MSA의 인스턴스들과 흐름등==
## MSA의 대표적인 4가지 큰 특징
### 1. Organized around Business Capabilites
- 비즈니스 특성에 따른 조직 구성을 할 수 있다는 장점
### 2. Decentralized Governance
- 단일 플랫폼이 아니다 라는 장점
- 팀이 스스로 기술 스택 표준을 선택할 수 있다.
### 3. Decentralized Data Management
- 데이터 관리의 분산
- 마이크로서비스간의 데이터베이스를 소유, 책임하여 스키마 충돌과 병목을 줄인다.
### 4. Design for failure
- 장애가 언제든 발생한다고 가정하고 서비스 연쇄 실패를 방지한다.
## MSA 변경으로 인해 발생가능한 Trade Off
### Trade Off
- 모니터링, 추상화, 성능, 복잡도 증가, 코드 중복방지등...
- DB는 원자성 보장과 분산 트랜잭션 관리가 어려워진다.
****
# 3. 📖 그래서 OpenTracing이 뭘까? (PDF 이론)
## 강의에서 사용하는 자료 입니다.
==자료 다운로드==
## 그래서 OpenTracing.. 너는 뭐니?
### OpenTracing 동작 방법
1. 환경에서 Request Path를 추적한다.
2. 어느 구간에서 병목이 발생하고 Request가 실패하였다면 어디에서 Error가 발생했는지 그에 따른 Critial Path가 무엇인지를 밝히는 작업
전통적인 모니터링 툴들은 아직 이 동작 방법에 적합한 툴이 없다.
## OpenTracing의 Basic Idea
### Basic Idea
- 각 단위, 단위의 프로세스 마다의 실행시간과 정보들을 Profiling하고
- 중앙에서 Profiling 정보를 모아서 Request 별로 관계를 재조합 한뒤에
- Visualization Tool 또는 분석해서 표기한다.
## OpenTracing Concepts
### Span
- OpenTracing에서 다루고 있는 가장 작은 작업 단위
- 일반 서비스 개발에서는 Context라는 개념으로 통상된다.
- 모든 Span은 Root Span을 기반으로 생성이 되며, 이후에 Root Span에 붙어서 생성이 되는 Span은 Child Span이라 한다.
- Span에 Tags, Baddage같은 옵션들을 붙여 추가적인 정ㅂ조를 주입할 수 있다.
### Trace
- 여러개의 Span을 담고 있는 하나의 작업
- Trace는 고유한 ID값이 존재하고, Trace를 담당하는 시스템을 말하기도 한다.
## OpenTracing Architecture
### Jaeger Architecture
#### Jaeger client
- 다양한 언어에 대해 OpenTracing 표준을 준수하는 SDK를 구현한다.
- 응용 프로그램은 API를 사용하여 데이터를 기록하여, 지정된 응용 프로그램에 따라 trace 정보를 Jaeger 에이전트로 전송한다.
#### Agent
- UDP포트를 사용해서, 수신된 Span 데이터를 모니터링하고 처리를 한다.
- 기본적인 구성요소이기 때문에, 모든 호스트에 배포가 된다.
#### Collector
- Agent로 부터 들어온 데이터를 수신하고, 저장소에 저장하는 역할을 수행한다.
- 원하는 아키텍처에 따라 `Kafka`, `Redis`를 활용하는 방법도 있다.
#### Data store
- 데이터를 저장하는 공간
- 원하는 저장소를 사용할 수 있으며 커스터마이징 가능
- 대표적으로 `ElasticSearch`를 많이 사용한다.
#### Query
- UI에 표기하기 위한 검색 툴
****
# 4. 🖥️ Golang을 통한 OpenTracing 다루기 (실습)
## 여러분들이 사용하셔야 하는 Docker 명령어 입니다.
`docker run --rm -p6831:6831/udp -p6832:6832/udp -p16686:16686 jaegertracing/all-in-one:1.60.0`
## Jaeger Tracer 생성 코드 다루기
==jaeger-client-go를 활용한 GlobalTrace 값 세팅==
## 많이 사용되는 OpenTracing 설정 값
==jaeger에서 자주 사용하는 설정값들 세팅==
## 간단한 API 구동 시키기
==gin을 활용한 서버 구동==
## Test Case를 위한 Router Path 설정하기
==Test를 위한 Router 등록, Router 등록을 위한 utils 작성==
## API를 통해서 가장 간단한 추적 만들어보기
==망할 강의에서 사용하는 jaegertracing/all-in-one 이미지가 버전업이되고 deprecated 될거라서 뭐 설명도 없고 1.60.0 에선 나오는데 1.68.0 에서는 안나오는데 설정법이나 이미지에 대한 설명이 싹 사라져서 원인을 찾기 힘들어 그냥 버전을 낮추는걸로 해결==
## 추가적인 Tag 주입하기 &amp; Child를 활용한 Span 주입하기
==Span을 계층적으로 추가하는 법과 Tag로 값을 보내는 방법==
## 다른 Host간에 추적을 위한 Request Header 정보 활용하기
==HTTP Header를 통해서 Span을 전달한다. 그래서 RootSpan에 아래 ChileSpan 계층이 계속 생겨나가게 된다.==
## Span에 Error 정보 심어보기
==Error의 정보를 넣어 jaeger의 표시가 다르게 되게끔 해주는 정도의 에러인데..?==
## Baggage를 통한 다른 Host간에 값 공유하기
==Tag는 단기 정보, Log는 이벤트용, Baggage는 장기 정보==
****
# 5. 🖥️ TypeScript를 활용한 OpenTracing 다루기 (실습)
## TypeScript에서는 이렇게 만들어 볼 예정입니다.
==Go project보다는 디테일하지 않더라도 Typescript로 opentracing을 작성할수 있고 그걸로 인사이트를 얻을 수 있을 정도의 강의가 될것이다.==
## Project 시작을 위한 Package Init
==express, jaeger-client, opentracing, ts-node 패키지 설치==
## Tracer 연결을 위한 코드 작성
****