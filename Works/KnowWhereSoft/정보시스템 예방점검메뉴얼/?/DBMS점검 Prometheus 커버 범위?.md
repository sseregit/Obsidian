### ✅ Prometheus로 점검할 수 있는 DB 항목

|점검 항목|가능 여부|사용 가능한 Exporter|
|---|---|---|
|**파일시스템 사용률 (DB 엔진, 아카이브 로그, 시스템 로그)**|✅ 가능|`node_exporter`|
|**메인 프로세스 기동 상태 점검 (smon 등)**|✅ 가능|`process_exporter`|
|**리스너 프로세스 기동 상태 점검**|✅ 가능|`process_exporter`|
|**DB 접속 상태 점검 (SQL 수행 가능 여부)**|✅ 가능|`postgres_exporter`, `mysqld_exporter`, `oracledb_exporter`|
|**물리적 메모리 사용률 점검**|✅ 가능|`node_exporter`|
|**물리적 CPU 사용률 점검**|✅ 가능|`node_exporter`|
|**DB 로그 점검 (Listener, Dump, 엔진 로그 등)**|✅ 가능|`promtail` + `Loki`|
|**DB 프로세스 개수 점검**|✅ 가능|`oracledb_exporter`, `postgres_exporter`, `mysqld_exporter`|
|**공유 메모리 (SGA) 설정값 점검**|✅ 가능|`oracledb_exporter`|
|**이중화 데이터 복제 정상 점검**|✅ 가능|`oracledb_exporter` (Data Guard 상태)|
|**컨트롤파일 이중화 점검**|❌ 불가능|Prometheus에서 직접 체크 불가 (DB 관리 도구 필요)|
|**리두로그 파일 이중화 점검**|❌ 불가능|Prometheus에서 직접 체크 불가 (DB 관리 도구 필요)|
|**테이블스페이스 사용률 점검**|✅ 가능|`oracledb_exporter`, `postgres_exporter`|
|**DB 백업 상태 점검 (RMAN, Exp 등)**|❌ 불가능|Prometheus에서 직접 체크 불가 (백업 관리 도구 필요)|
|**온라인 백업 가능 여부 점검 (아카이브 모드 활성화 여부)**|✅ 가능|`oracledb_exporter` (아카이브 모드 상태 체크)|
|**환경설정 파일 백업 점검**|❌ 불가능|Prometheus에서 직접 체크 불가 (파일 모니터링 도구 필요)|
|**트랜잭션 로그 사이즈 점검**|✅ 가능|`oracledb_exporter`, `postgres_exporter`|

---

### 📌 세부 설명

1. **파일시스템 사용률 점검**
    
    - `node_exporter`를 활용하여 DB 엔진이 설치된 파일시스템, 아카이브 로그 저장 공간, 시스템 로그 저장 공간의 사용률을 확인 가능.
2. **DB 프로세스 및 리스너 상태 점검**
    
    - `process_exporter`를 활용하여 Oracle `smon`, `pmon`, `tnslsnr` 프로세스가 정상적으로 실행 중인지 모니터링 가능.
3. **DB 접속 상태 점검**
    
    - `oracledb_exporter`, `postgres_exporter`, `mysqld_exporter`를 활용하여 DB 커넥션이 정상적으로 작동하는지 SQL 커맨드를 수행하여 점검 가능.
4. **SGA 및 프로세스 개수 점검**
    
    - `oracledb_exporter`를 활용하여 SGA 메모리 사용률 및 최대 프로세스 개수 대비 사용량을 확인 가능.
5. **이중화 점검**
    
    - `oracledb_exporter`를 이용해 Oracle Data Guard 상태를 모니터링하여 Active-Standby 구성의 데이터 복제가 정상적으로 수행되는지 확인 가능.
    - 다만, 컨트롤파일 및 리두로그 파일의 물리적 이중화 상태는 Prometheus에서 직접 모니터링할 수 없음.
6. **테이블스페이스 사용률 점검**
    
    - `oracledb_exporter`에서 테이블스페이스 사용량을 90% 초과하는 경우 알람을 설정하여 모니터링 가능.
7. **트랜잭션 로그 사이즈 점검**
    
    - `oracledb_exporter`, `postgres_exporter`를 활용하여 트랜잭션 로그의 크기를 확인하고, 무한정 증가하는 경우 경고 설정 가능.

---

### ❌ Prometheus로 직접 확인하기 어려운 항목

- **컨트롤파일 및 리두로그 파일 이중화 점검**
    
    - Prometheus에서는 물리적 파일의 복제 상태를 직접 확인할 수 없음.
    - DB 관리 도구 (Oracle RMAN, Data Guard) 또는 스크립트를 통해 주기적으로 체크해야 함.
- **DB 백업 상태 점검 (RMAN, Exp 등)**
    
    - Prometheus는 백업 프로세스를 직접 감지할 수 없음.
    - 백업 로그를 `promtail` + `Loki`로 분석하거나, DB 백업 스케줄러와 연동해야 함.
- **환경설정 파일 백업 점검**
    
    - Prometheus에서 파일의 변경 내역을 추적할 수 없음.
    - `auditd` 또는 `inotify`를 이용한 파일 모니터링 필요.

---

### 🔥 결론

- Prometheus의 `oracledb_exporter`, `postgres_exporter`, `node_exporter`, `process_exporter`, `promtail + Loki` 등을 활용하면 대부분의 DB 모니터링이 가능함.
- 하지만, **컨트롤파일 이중화, 리두로그 파일 이중화, 백업 상태 점검, 환경설정 파일 백업 점검** 등은 Prometheus에서 직접 확인하기 어려우므로 별도의 관리 도구와 연계해야 함.