[Long polling: What it is and when to use it](https://sendbird.com/developer/tutorials/what-is-long-polling?utm_source=chatgpt.com)
[What is Server Sent Event(SSE) and How to Use It in Java Spring Boot?](https://medium.com/codimis/what-is-server-sent-event-sse-and-how-to-use-it-in-java-spring-boot-7f4ffa828882)
[Server-Sent Events, WebSockets, and HTTP](https://www.mnot.net/blog/2022/02/20/websockets)
# Server-sent events(SSE)
- 서버 -> 클라이언트 방향의 단방향 통신 모델로, 단일의 장시간 지속되는 연결을 통해 업데이트를 전달한다.
- **클라이언트는 데이터를 받을 수만 있고, 서버로 데이터를 보낼 수 없다**
	- 채팅이나 비디오 게임처럼 클라이언트 측 상호작용이 필요한 애플리케이션에 적합하지 않다.
- HTTP/1.1과 잘 작동하지 않으며, 그 주된 이유는 연결 수 제한 때문이다.
- TCP의 Head-of-Line 블로킹 현상때문에 패킷이 손실되면 이후 패킷들은 무기한 대기 상태에 빠질 수 있다.