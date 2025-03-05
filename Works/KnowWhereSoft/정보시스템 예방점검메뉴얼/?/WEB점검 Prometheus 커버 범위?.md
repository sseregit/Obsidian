다음은 **1.1.2 WEB 점검 리스트**에 대해 **Linux 환경에서 Prometheus를 활용하여 점검할 수 있는 항목과 불가능한 항목을 포함한 표**입니다.

---

### **📋 1.1.2 WEB 점검 리스트 (Linux 기준, Prometheus 활용 가능 여부 포함)**

|**구분**|**세부 점검 항목**|**설명**|**Prometheus 사용 가능 여부**|**사용할 Exporter**|
|---|---|---|---|---|
|**① 프로세스**|①-1 프로세스 CPU 사용률|WEB 프로세스가 사용하고 있는 CPU 자원 사용률 확인|✅ 가능|`node_exporter`|
||①-2 프로세스 메모리 사용률|WEB 프로세스가 사용하고 있는 메모리 자원 사용률 확인|✅ 가능|`node_exporter`|
||①-3 프로세스 사용 상태 점검|점유 리소스 사용률 점검|✅ 가능|`node_exporter`|
||①-4 프로세스 기동 점검|WEB 프로세스가 정상적으로 기동되었는지 점검|❌ 불가능|OS 명령어 필요 (`systemctl status httpd`)|
|**② 파일시스템**|②-1 WEB 엔진 파일시스템 점검|WEB 엔진 설치 파일시스템 FULL 여부 점검|✅ 가능|`node_exporter`|
||②-2 WEB 어플리케이션 설치 파일시스템 점검|WEB 소스가 설치된 파일시스템 FULL 여부 점검|✅ 가능|`node_exporter`|
||②-3 WEB 로그 저장 파일시스템 점검|Access Log, Error Log 저장 파일시스템 FULL 여부 점검|✅ 가능|`node_exporter`|
|**③ 서비스**|③-1 서비스 포트 오픈 상태 점검|WEB 프로세스 기동 시 생성된 포트가 정상적으로 오픈되었는지 점검|✅ 가능|`blackbox_exporter` (TCP 포트 체크)|
||③-2 서비스 포트 접속 정상 확인|출발지 IP에서 목적지 IP 포트로 정상적으로 접속되는지 점검|✅ 가능|`blackbox_exporter` (ICMP/TCP 포트 테스트)|
||③-3 사용자 요청량 처리 수 점검|WEB 서비스의 요청량 및 환경설정 값이 적절한지 확인|✅ 부분 가능|`apache_exporter` (Apache), `nginx_exporter` (Nginx)|
|**④ 환경설정**|④-1 WEB-WAS 연동 상태 점검|WEB-WAS 커넥션 상태 지속 여부 확인|❌ 불가능|OS 명령어 필요 (`curl`, `netstat`)|
|**⑤ 로그**|⑤-1 접근 로그 점검|사용자 요청 정상 처리 여부 확인 (HTTP 200 응답 확인)|❌ 불가능|OS 명령어 필요 (`grep "200" /var/log/httpd/access.log`)|
||⑤-2 연동 결과 로그 점검|WAS 연동 결과 및 수행 시간 확인|❌ 불가능|OS 명령어 필요 (`grep "response time" /var/log/httpd/access.log`)|
||⑤-3 에러 로그 점검|서버 오류(HTTP 500, 503 등) 발생 여부 확인|❌ 불가능|OS 명령어 필요 (`grep "500\|503" /var/log/httpd/error.log`)|
|**⑥ 서비스 상태 점검**|⑥-1 요청 문서 처리 불가 점검|404 Not Found 등 웹페이지 제공 불가 여부 확인|❌ 불가능|OS 명령어 필요 (`grep "404" /var/log/httpd/access.log`)|
||⑥-2 WEB 서비스 불가 점검|500 Internal Server Error 등 서비스 불가 여부 점검|❌ 불가능|OS 명령어 필요 (`grep "500" /var/log/httpd/error.log`)|
||⑥-3 서비스 제공 불가 점검|503 Service Unavailable 등 웹 서버 응답 실패 점검|❌ 불가능|OS 명령어 필요 (`grep "503" /var/log/httpd/error.log`)|

---

### **📌 설명**

- ✅ **가능:** Prometheus 및 해당 Exporter를 사용하여 점검 가능.
- ✅ **부분 가능:** 일부 항목을 모니터링할 수 있으나, 추가적인 설정 또는 외부 도구 필요.
- ❌ **불가능:** Prometheus에서 직접 점검할 수 없음. OS 명령어나 추가적인 모니터링 솔루션 필요.

---

### **🔹 결론**

✅ **Linux 환경에서 `node_exporter`, `blackbox_exporter`, `apache_exporter`, `nginx_exporter` 등을 활용하여 WEB 서버 주요 성능 모니터링 가능**  
✅ **WEB 프로세스, 파일시스템, 포트 오픈 상태, 사용자 요청량 모니터링 가능**  
❌ **WEB 로그 분석, 서비스 오류 점검(404, 500, 503 등)은 Prometheus에서 직접 확인 불가 (OS 명령어나 추가 도구 필요)**

이 정보를 기반으로 **Prometheus 기반의 Linux WEB 서버 모니터링을 구성할 수 있습니다**.  
필요하면 **Grafana 대시보드 설정이나 PromQL 쿼리**도 추가로 제공해드릴 수 있어요! 🚀😊