[Long polling: What it is and when to use it](https://sendbird.com/developer/tutorials/what-is-long-polling?utm_source=chatgpt.com)
[웹 브라우저에서 통신 방법(Polling, Long Polling, Streaming, Socket)](https://warmth424.tistory.com/18)
# Polling
## 장점
- 일정하게 갱신되는 서버 데이터의 경우 유용하게 사용될 수 있는 방식
## 단점
- Client가 많아지면 Server의 부담이 급증
- Client 측에서 실시간 정도의 빠른 응답을 기대하기 어려움.
- HTTP 오버헤드 (전송하는 데이터 양에 비해 header의 양이 큰 문제)발생.