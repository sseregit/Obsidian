### ✅ Prometheus로 점검할 수 있는 WAS 항목

|점검 항목|가능 여부|사용 가능한 Exporter|
|---|---|---|
|**프로세스 CPU 사용률**|✅ 가능|`process_exporter`, `node_exporter`|
|**프로세스 메모리 사용률**|✅ 가능|`process_exporter`, `node_exporter`|
|**프로세스 사용 상태 점검**|✅ 가능|`process_exporter`|
|**프로세스 기동 상태 점검 (컨테이너 포함)**|✅ 가능|`process_exporter`, `cadvisor`, `blackbox_exporter`|
|**로그 점검 (접속기록, 메모리, 커넥션풀 누수 등)**|✅ 가능|`promtail` + `Loki`|
|**JVM Heap Memory 사용량 점검**|✅ 가능|`jmx_exporter`|
|**Thread Pool 설정값 초과 여부 점검**|✅ 가능|`jmx_exporter`|
|**장기 수행 작업 확인**|✅ 가능|`jmx_exporter`|
|**DB Connection Pool 설정값 초과 여부**|✅ 가능|`jmx_exporter`, `postgres_exporter`, `mysqld_exporter`|
|**DB 연결 상태 점검**|✅ 가능|`jmx_exporter`, `postgres_exporter`, `mysqld_exporter`|
|**HeapDump 파일 발생 여부 확인**|✅ 가능|`jmx_exporter`, `promtail` + `Loki` (로그 분석)|
|**소스 Deploy 상태 점검**|❌ 불가능|직접적인 모니터링 불가 (배포 자동화 툴과 연계 필요)|
|**서비스 평균 처리시간 점검**|✅ 가능|`jmx_exporter`, `nginx_exporter`, `apache_exporter`|
|**기동 스크립트 변경 여부 확인**|❌ 불가능|Prometheus에서 직접 감지 불가 (CI/CD 또는 파일 모니터링 필요)|

---

### 📌 세부 설명

1. **JVM 관련 모니터링**
    
    - `jmx_exporter`를 활용하면 Heap Memory, Thread Pool, Connection Pool을 모니터링할 수 있음.
    - `java.lang:type=Memory` 및 `java.lang:type=Threading` MBean을 활용하여 JVM 상태를 체크 가능.
2. **DB Connection Pool 모니터링**
    
    - `jmx_exporter`를 이용해 HikariCP, Tomcat JDBC Connection Pool 등의 상태를 확인 가능.
    - DB 자체의 연결 상태는 `postgres_exporter`, `mysqld_exporter` 등을 활용.
3. **HeapDump 파일 확인**
    
    - `jmx_exporter`로 Heap 사용량을 지속적으로 모니터링.
    - `promtail` + `Loki`를 활용하면 특정 에러 로그를 탐지하여 HeapDump 발생 여부를 감지 가능.
4. **컨테이너 기반 WAS 모니터링**
    
    - `cadvisor`를 이용하면 컨테이너 내에서 실행 중인 WAS의 CPU, 메모리 사용량을 쉽게 모니터링 가능.
    - `blackbox_exporter`를 활용해 WAS 프로세스의 정상 기동 여부 확인 가능.

---

### ❌ Prometheus로 직접 확인하기 어려운 항목

- **소스 배포 상태 (Deploy 상태 확인)**
    - 배포 자동화 툴 (예: ArgoCD, Jenkins, GitOps)과 연계하여 상태 체크 필요.
- **기동 스크립트 변경 여부 확인**
    - Prometheus는 파일 변경 감지를 지원하지 않음.
    - `auditd`, `inotify` 또는 CI/CD 파이프라인을 활용하여 체크 필요.

---

### 🔥 결론

Prometheus의 `jmx_exporter`, `node_exporter`, `process_exporter`, `cadvisor`, `blackbox_exporter`, `Loki` 등을 활용하면 대부분의 WAS 모니터링이 가능함. 하지만, 소스 배포 상태 및 기동 스크립트 변경 사항은 별도의 툴과 연계해야 함.