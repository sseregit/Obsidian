- Event Sourcing의 개념
	- [이벤트 소싱 개념](https://sddev.tistory.com/111)
	- [이벤트 소싱 event-sourcing 패턴 정리](https://edykim.com/ko/post/eventsourcing-pattern-cleanup/)
- [CQRS](https://bluayer.com/37)
	- Command and Query Responsibility Segregation

- [배달의 민족 마이크로서비스 여행기](https://www.youtube.com/watch?v=BnS6343GTkY)
- [대용량 처리를 위한 서비스 구성](https://jistol.github.io/architecture/2017/02/14/architecture-traffic-issue/)
- [EventStore](https://cla9.tistory.com/14)

### 답변
- 이벤트 소싱
	- 이벤트에 의해 구동되는 데이터 작업 처리 방법
	- 이벤트 사용으로 인한 구현 및 관리를 간소화 할수 있다.
	- 모든 상태 변경이 이벤트로 캡처 되므로 수행된 모든 작업에 대한 감사 추적을 제공받는다.
- CQRS
	- 데이터 저장소에 대한 읽기 및 업데이트 작업을 구분하는 패턴인 명령과 쿼리의 역할 분리를 의미한다.