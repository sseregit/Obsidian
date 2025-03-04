Prometheus에서 사용할 수 있는 Exporter들을 포함하여, 모니터링 가능 여부를 정리했습니다.  

---

## ✅ Prometheus로 점검할 수 있는 항목  

### ① 프로세스  
- **프로세스 CPU 사용률** → `node_exporter` + `process_exporter`  
  - `process_cpu_seconds_total` 또는 `node_cpu_seconds_total`을 활용하여 특정 프로세스의 CPU 사용률 확인 가능  
- **프로세스 메모리 사용률** → `node_exporter` + `process_exporter`  
  - `process_resident_memory_bytes` 또는 `node_memory_*` 메트릭 활용 가능  
- **프로세스 사용 상태 점검** → `process_exporter`  
  - 특정 프로세스의 존재 여부 및 리소스 사용률 점검 가능  
- **프로세스 기동 점검** → `process_exporter` + `blackbox_exporter`  
  - 프로세스가 실행 중인지 확인 가능 (`process_start_time_seconds`)  

### ② 파일시스템 점검  
- **WEB 엔진 파일시스템 점검** → `node_exporter`  
  - `node_filesystem_avail_bytes`, `node_filesystem_size_bytes`를 사용해 파일 시스템 사용률 점검 가능  
- **WEB 어플리케이션 설치 파일시스템 점검** → `node_exporter`  
  - 동일한 파일 시스템 메트릭 활용 가능  
- **WEB 로그 저장 파일시스템 점검** → `node_exporter`  
  - 로그 저장 디렉토리의 사용률 점검 가능  

### ③ 서비스  
- **서비스 포트 오픈 상태 점검** → `blackbox_exporter`  
  - 특정 포트가 열려 있는지 `TCP` 모드를 사용해 확인 가능  
- **서비스 포트 접속 정상 확인** → `blackbox_exporter`  
  - 출발지에서 목적지 포트로의 연결 상태를 `ICMP` 또는 `TCP` 테스트로 점검 가능  
- **사용자 요청량 처리 수 점검** → `nginx_exporter`, `apache_exporter` 등  
  - 웹서버 요청 처리량을 수집하여 적절한 설정값 검토 가능  

### ④ 환경설정  
- **WEB-WAS 연동 상태 점검** → `blackbox_exporter` + `jmx_exporter`  
  - WAS(예: Tomcat)의 커넥션 상태를 `JMX`에서 확인하거나 `blackbox_exporter`를 이용해 HTTP 응답 상태 점검 가능  

### ⑤ 로그  
- **로그 점검** → `promtail` + `Loki`  
  - 웹 서버 접속 로그, 서비스 수행 시간, 에러 로그 등을 수집하여 분석 가능  

---

## ❌ Prometheus로 직접 점검하기 어려운 항목  

### ① 프로세스  
- **웹 프로세스 부하 원인 분석**  
  - Prometheus는 리소스 사용률을 측정할 수 있지만, 부하가 발생하는 원인(예: 코드 최적화 필요 여부)은 확인할 수 없음  

### ② 파일시스템  
- **파일 시스템 오류 또는 손상 여부**  
  - Prometheus는 사용률 모니터링은 가능하지만, 파일 시스템의 손상 여부(`fsck` 결과) 등은 확인 어려움  

### ③ 서비스  
- **방화벽 또는 보안장비 차단 여부 상세 분석**  
  - `blackbox_exporter`를 이용해 연결 여부는 확인할 수 있지만, 방화벽 정책에 의해 차단되었는지까지 확인하려면 추가적인 로그 분석 필요  

### ④ 환경설정  
- **HTTPS 보안 설정 검토**  
  - `blackbox_exporter`를 이용해 인증서 만료 여부는 확인할 수 있지만, 보안 설정(TLS 버전, 취약점 등)은 별도 스캐너 필요  

---

### 📌 결론  
Prometheus는 `node_exporter`, `process_exporter`, `blackbox_exporter`, `nginx_exporter`, `apache_exporter`, `jmx_exporter`, `Loki` 등을 조합하면 대부분의 모니터링이 가능합니다. 하지만, 파일 시스템 손상 여부, 방화벽 설정, HTTPS 보안 설정 등은 Prometheus만으로 직접 확인하기 어렵습니다.