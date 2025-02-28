# Pushgateway

배치 job에서 가장 최근에 push한 메트릭을 저장한다.
덕분에 프로메테우스는 배치 job이 종료된 후에도 관련 메트릭을 스크랩할 수 있다.

**Prometheus는 특정한 제한된 경우에만 사용할 것을 추천한다..**

일반적인 메트릭 수집에 Prometheus의 기본적인 풀(Pull) 모델 대신 Pushgateway를 무분별하게 사용하면 몇 가지 문제점이 있다.

- 단일 장애 지점 및 병목 현상
	- 여러 인스턴스를 단일 Pushgateway를 통해 모니터링하면, Pushgateway가 단일 장애 지점이자 잠재적인 별목이 될 수 있다.
- 인스턴스 상태 모니터링 손실
	- Prometheus의 `up`메트릭(스크랩 시마다 생성됨)을 통한 자동 인스턴스 상태 모니터링 기능을 잃게 된다.
- 메트릭의 영구 노출
	- Pushgateway는 푸시된 시계열을 절대 잊지 않으며, Pushgateway의 API를 통해 수동으로 삭제하지 않는한 해당 시계열을 Prometheus에 영구적으로 노출한다.

2025-02-28
정보시스템의 부서 단위로 Pushgateway를 쓰는것이 좋아 보였는데 일단 **보류**!

[### Pushing metrics (번역)](https://godekdls.github.io/Prometheus/practices.pushing/)
[# When to use the Pushgateway](https://prometheus.io/docs/practices/pushing/)