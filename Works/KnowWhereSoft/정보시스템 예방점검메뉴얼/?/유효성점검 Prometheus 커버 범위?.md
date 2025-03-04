### ✅ Prometheus로 점검할 수 있는 시스템 항목

|점검 항목|가능 여부|사용 가능한 Exporter|
|---|---|---|
|**NTP 시간 점검 (현재 시간 불일치 확인)**|✅ 가능|`node_exporter` (시스템 시간 메트릭)|
|**SSL 인증서 유효기간 점검**|✅ 가능|`blackbox_exporter` (SSL 인증서 만료일 확인)|
|**라이선스 점검 (정식/임시 라이선스 유효기간 확인)**|✅ 가능 (일부 SW에 한정)|`node_exporter` (파일 존재 여부), Custom Exporter|
|**도메인 점검 (도메인 만료일 점검 및 서비스 불가 방지)**|✅ 가능|`blackbox_exporter` (DNS 조회 및 응답 확인)|

---

### 📌 세부 설명

1. **NTP 시간 점검**
    
    - `node_exporter`에서 제공하는 `node_time_seconds` 메트릭을 사용하여 서버 시간이 정상인지 확인 가능.
    - NTP 동기화 여부를 주기적으로 확인하여 시간 불일치 감지 가능.
2. **SSL 인증서 유효기간 점검**
    
    - `blackbox_exporter`의 `ssl_expiry` 메트릭을 활용하여 SSL 인증서 만료일을 지속적으로 모니터링 가능.
    - 특정 임계값(예: 30일 이하)에서 알람을 발생시켜 인증서 갱신 필요 여부 파악 가능.
3. **라이선스 점검**
    
    - 일부 라이선스는 파일이나 환경 변수로 저장되므로 `node_exporter`의 파일 존재 여부 체크 기능을 활용할 수 있음.
    - 라이선스 만료일이 특정 명령어(`license status` 등)로 조회 가능하면 Custom Exporter를 만들어 모니터링 가능.
4. **도메인 점검**
    
    - `blackbox_exporter`를 활용하여 도메인 만료일 점검 가능.
    - DNS 응답 상태를 확인하여 도메인이 정상적으로 작동하는지 모니터링 가능.
    - WHOIS 정보를 조회하여 도메인 갱신 필요 여부를 확인하는 Custom Exporter도 활용 가능.

---

### 🔥 결론

- `node_exporter`, `blackbox_exporter`, 그리고 Custom Exporter를 활용하면 **시간 동기화, SSL 인증서 만료, 라이선스 만료, 도메인 만료** 등의 주요 위험 요소를 사전에 감지 가능.
- Prometheus AlertManager를 활용하면 특정 기준 (예: SSL 인증서 30일 이하, NTP 시간 불일치) 시 **자동 알람 발송** 가능.