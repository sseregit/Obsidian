## HTTP 1.0
- Resource를 가져올때마다 TCP/IP연결을 해야했다.

## HTTP 1.1
- Resource를 가져올때 마다 하던 연결을 1회만 하게 되었다.
	- HTTP, CSS, JS.... 다 가져와서 연결을 끊는다.
- Request에 순서대로 데이터가 전송된다.

## HTTP 2.0
- **SPDY** -> HTTP 2.0
- 멀티세션 같은 개념을 지원 I/O 멀티 플렉싱이 가능하다.
	- [HTTP1.0과 HTTP2.0의 비교](https://www.httpvshttps.com)
- Binary framing layer

## HTTP 3.0
- UDP