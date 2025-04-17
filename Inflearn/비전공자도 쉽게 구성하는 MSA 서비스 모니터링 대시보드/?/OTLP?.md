# OTLP(OpenTelemetry Protocol)
- OpenTelemetry가 사용하는 데이터 전송 프로토콜
- 주로 분산 추적(Trace), 메트릭(Metric), 로그(Log)데이터를 전송하는데 사용된다.
### 특징
- 주로 [[gRPC?]] 또는 HTTP(Proto/JSON)방식을 통해 데이터를 전송한다.
- 표준화된 프로토콜로, 다양한 언어와 도구 간의 높은 호환성을 제공한다.

### 주요 구성
#### OTLP-gRPC
- 주로 쓰는 포트 4317
- gRPC 기반 프로토콜
#### OTLP-HTTP
- 주로 쓰는 포트 4318
- HTTP 기반 프로토콜 (주로 JSON 형식)