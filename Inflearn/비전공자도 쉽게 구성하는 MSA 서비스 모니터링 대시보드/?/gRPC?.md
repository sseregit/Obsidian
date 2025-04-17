# gRPC
- 구글이 개발한 고성능 원격 프로시저 호출(Remote Procedure Call)프레임워크
- 주로 서버 간 통신에 사용되며, 네트워크를 통해 메서드를 호출하는 방식으로 데이터를 주고 받는다.
- 내부적으로 TCP/IP 기반의 통신을 사용하며, 데이터는 **Protocol Buffers**로 직렬화 된다.
### 특징
- 빠르고 효율적인 통신 가능
- 명확하게 정의된 API 명세
- 양방향 스트리밍 지원
- 다양한 언어 지원
### 핵심 구성
#### Protocol Buffers (ProtoBuf)
- 데이터를 직렬화 하는 방식
- JSON이나 XML보다 효율적이고 빠름
- 명확한 데이터 타입을 미리 정의(.proto 파일)
#### HTTP/2
- HTTP/2 기반으로 데이터를 주고받아 통신 성능 향상
- 하나의 연결(connection)에 여러 요청을 동시에 처리
- 낮은 지연(Low latency), 높은 성능(High Performance) 보장