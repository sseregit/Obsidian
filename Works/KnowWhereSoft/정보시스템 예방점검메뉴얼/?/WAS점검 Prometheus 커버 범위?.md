다음은 **1.1.3 WAS 점검 리스트**에 대해 **Linux 환경에서 Prometheus를 활용하여 점검할 수 있는 항목과 불가능한 항목을 포함한 표**입니다.

---

### **📋 1.1.3 WAS 점검 리스트 (Linux 기준, Prometheus 활용 가능 여부 포함)**

|**구분**|**세부 점검 항목**|**설명**|**Prometheus 사용 가능 여부**|**사용할 Exporter**|
|---|---|---|---|---|
|**① 프로세스**|①-1 프로세스 CPU 사용률|WAS 서비스 부하 확인을 위한 CPU 사용률 점검|✅ 가능|`node_exporter`|
||①-2 프로세스 메모리 사용률|WAS 서비스 부하 확인을 위한 메모리 사용률 점검|✅ 가능|`node_exporter`|
||①-3 프로세스 사용 상태 점검|WAS 프로세스 점유 리소스 사용률 점검|✅ 가능|`node_exporter`|
||①-4 프로세스 기동 상태 점검|서비스 컨테이너별 WAS 프로세스 정상 구동 여부 점검|❌ 불가능|OS 명령어 필요 (`systemctl status tomcat`)|
|**② 로그**|②-1 로그 점검|관리서버, 서비스, 클라이언트 접속 기록, 메모리, 커넥션풀 누수 발생 여부 점검|❌ 불가능|OS 명령어 필요 (`grep` 활용 로그 분석)|
|**③ JVM Heap Memory**|③-1 Heap Memory 점검|Java Heap 메모리 여유 공간 점검 (GC 발생 빈도 및 메모리 부족 예방)|✅ 가능|`jmx_exporter` (JVM 메트릭 수집)|
|**④ Thread Pool 상태**|④-1 Work Thread Pool 점검|설정된 Max Thread 값과 현재 사용량 점검|✅ 가능|`jmx_exporter`|
||④-2 장기 수행 작업 확인|장시간 대기 중인 Thread 존재 유무 점검|✅ 부분 가능|`jmx_exporter` (JVM 메트릭 분석 필요)|
|**⑤ Connection Pool 상태**|⑤-1 DB 연결 객체 저장공간 초과 여부 점검|Connection Pool 설정값 초과 여부 점검|✅ 가능|`jmx_exporter`|
||⑤-2 DB 연결 상태 점검|Connection Pool 내부 DB 연결 정상 여부 점검|✅ 가능|`jmx_exporter`|
|**⑥ 서비스 성능 및 설정 점검**|⑥-1 평균 처리 시간 점검|WAS의 평균 요청 처리 시간 점검|✅ 가능|`jmx_exporter` (JVM 메트릭 활용)|
||⑥-2 기동 스크립트 확인|WAS 기동 스크립트 정상 실행 여부 점검|❌ 불가능|OS 명령어 필요 (`stat /path/to/startup.sh`)|
|**⑦ 서비스 상태 점검**|⑦-1 서비스 포트 오픈 상태 점검|WAS 서비스 포트 정상적으로 Listen 상태 유지 여부 점검|✅ 가능|`blackbox_exporter` (TCP 포트 체크)|
||⑦-2 서비스 포트 접속 정상 확인|출발지 IP에서 목적지 WAS IP 포트 정상 접속 여부 점검|✅ 가능|`blackbox_exporter` (ICMP/TCP 포트 테스트)|
||⑦-3 요청 문서 처리 불가 점검|404 Not Found 발생 여부 점검|❌ 불가능|OS 명령어 필요 (`grep "404" /path/to/access.log`)|
||⑦-4 WAS 서비스 불가 점검|500 Internal Server Error 발생 여부 점검|❌ 불가능|OS 명령어 필요 (`grep "500" /path/to/error.log`)|
||⑦-5 서비스 제공 불가 점검|503 Service Unavailable 발생 여부 점검|❌ 불가능|OS 명령어 필요 (`grep "503" /path/to/error.log`)|

---

### **📌 설명**

- ✅ **가능:** Prometheus 및 해당 Exporter를 사용하여 점검 가능.
- ✅ **부분 가능:** 일부 항목을 모니터링할 수 있으나, 추가적인 설정 또는 외부 도구 필요.
- ❌ **불가능:** Prometheus에서 직접 점검할 수 없음. OS 명령어나 추가적인 모니터링 솔루션 필요.

---

### **🔹 결론**

✅ **Linux 환경에서 `node_exporter`, `jmx_exporter`, `blackbox_exporter` 등을 활용하여 WAS 성능 및 주요 상태 모니터링 가능**  
✅ **WAS 프로세스 리소스 사용률, JVM Heap 메모리, Connection Pool, Thread Pool 등은 Prometheus 기반으로 모니터링 가능**  
❌ **로그 분석, 404/500/503 오류 감지는 Prometheus에서 직접 수행 불가능 (OS 명령어나 ELK 스택 필요)**

이 정보를 기반으로 **Prometheus 기반의 Linux WAS 모니터링을 구성할 수 있습니다**.  
필요하면 **Grafana 대시보드 설정이나 PromQL 쿼리**도 추가로 제공해드릴 수 있어요! 🚀😊