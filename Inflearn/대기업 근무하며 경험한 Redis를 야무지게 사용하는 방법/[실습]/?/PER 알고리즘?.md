# PER(Pipelined Execution of Redis) 알고리즘
- `Redis`명령을 파이프라인 방식으로 묶어 한 번에 전송하여, 네트워크 왕복 비용(RTT, Round Trip Time)을 줄이는 최적화 기법
- Redis 자체 알고리즘이 아니라, Redis 클라이언트에서 사용하는 **통신 방식 최적화 전략** 이다.
