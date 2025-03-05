# 리액티브 스트림
- 비동기 데이터 스트림을 처리하기 위한 표준 사양
- 즉, 데이터가 발생하는 생산자(Publisher)와 이를 소비하는 구독자(Subscriber)간의 비동기적, 논블로킹 방식의 데이터 처리를 정의한 인터페이스

## 리액티브 스트림의 4가지 핵심 인터페이스
1. `Publisher<T>`
	- 데이터를 생산하는 역할 (생산자)
	- `subscribe(Subscribe<T> subscriber)`메서드를 통해 구독자를 등록
	- 여러 개의 `Subscriber`와 연결 가능
2. `Subscriber<T>`
	- 데이터를 소비하는 역할 (구독자)
	- `onNext()`, `onError()`, `onComplete()`등의 메서드를 구현하여 응답을 받음
3. `Subscription`
	- Publisher와 Subscriber 사이에서 데이터 흐름을 조절하는 역할
	- `request(n)`
		- 구독자가 처리할 수 있는 만큼의 데이터를 요청
	- `cancel()`
		- 데이터 스트림을 취소
4. `Processor`
	- Publisher와 Subscriber 역할을 모두 수행하는 중간 처리자
	- 데이터를 변환하거나 중간에서 가공하는 역할