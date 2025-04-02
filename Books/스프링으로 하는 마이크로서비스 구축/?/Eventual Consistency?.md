# Eventual Consistency
- 시스템의 각 구성요소가 즉시 일관된 상태를 유지하지는 않지만, **일정 시간이 지난 후에는 결국(consistently)같은 상태에 도달하게 된다**는 개념

|**패턴**|**설명**|
|---|---|
|**Outbox Pattern**|DB 트랜잭션과 이벤트 발행을 분리하되 원자성 보장|
|**Polling Publisher**|DB에 저장된 이벤트를 주기적으로 읽어 큐로 발행|
|**Saga Pattern**|마이크로서비스 간 트랜잭션 보상/조정 처리|
|**Retry / DLQ**|실패한 메시지는 재시도 또는 사후 처리|
