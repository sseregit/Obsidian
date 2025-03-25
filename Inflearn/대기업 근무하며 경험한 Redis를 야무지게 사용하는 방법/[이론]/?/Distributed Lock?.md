# 분산 락(Distributed Lock)
- 서로 다른 서버 또는 프로세스들이 공통 자원(shared resource)에 동시에 접근하지 못하도록 보장하는 락(Lock)
### 목적
- 여러 서버 간 데이터 일관성을 유지하고, 동시성 제어(concurrency control)를 수행
### 필요한 이유
- 분산 환경에서는 단일 서버 환경과 달리 기존의 JVM내에서 사용하는 lock(synchronized, ReentrantLock 등)으로는 충분히 보장할 수 없기 때문에.
