- Event Sourcing의 개념
	- [이벤트 소싱 개념](https://sddev.tistory.com/111)
	- [이벤트 소싱 event-sourcing 패턴 정리](https://edykim.com/ko/post/eventsourcing-pattern-cleanup/)
- [CQRS](https://bluayer.com/37)
	- Command and Query Responsibility Segregation

- [배달의 민족 마이크로서비스 여행기](https://www.youtube.com/watch?v=BnS6343GTkY)
- [대용량 처리를 위한 서비스 구성](https://jistol.github.io/architecture/2017/02/14/architecture-traffic-issue/)
- [EventStore](https://cla9.tistory.com/14)

### Event Sourcing
- 데이터 저장 방식의 한 종류이다.
- 이벤트 소싱 패턴은 **일련의 이벤트를 통해 데이터를 조작하는 접근 방식이다.**
	- 데이터에 영향을 주는 모든 동작을 이벤트라는 저수준의 데이터로 관리하는 것으로 여러 문제를 해결할 수 있다. 단점도 여러가지 존재한다.