[What is Pub/Sub? The Publish/Subscribe model explained](https://ably.com/topic/pub-sub?utm_source=chatgpt.com)
[Pub/Sub pattern architecture](https://ably.com/topic/pub-sub-architecture)
[What are the benefits of Pub/Sub messaging?](https://ably.com/topic/pub-sub-benefits)
[Publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern?utm_source=chatgpt.com)
# Pub/Sub Model
- 분산 시스템에서 서로 다른 구성 요소나 서비스 간의 비동기 통신을 위해 사용 되는 아키텍처 설계 패턴
- 특징의 핵심은 Pub/Sub이 시스템 내 서로 다른 구성 요소들이 서로의 정체성을 알지 못한 채 메시지를 주고받을 수 있게 해준다는 점(디커플링 되어있다.)
- 발행자가 구독자의 응답을 기다리지 않는 비동기 통신을 위해 설계되었다.
## 장점
- 느슨한 결합(Loose coupling)
	- 퍼블리셔는 서브스크라이버와 느슨하게 결합되어 있으며, 존재를 알 필요가 없다.
- 확장성
	- 병렬 처리, 메시지 캐싱, 트리 기반 또는 네트워크 기반 라우팅 등의 방법으로 기존 클라이언트-서버 모델보다 더 나은 확장성을 제공할 수 있다.
- 메시지 전달 문제
	- 중복된 서브스크라이버를 사용하면, 복잡도를 거의 증가시키지 않고도 메시지 전달 보장을 도울 수 있다.