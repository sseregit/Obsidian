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
****
# 4. 🖥️ Golang을 통한 OpenTracing 다루기 (실습)

****
# 5. 🖥️ TypeScript를 활용한 OpenTracing 다루기 (실습)

****