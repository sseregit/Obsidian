### ✅ Prometheus로 점검할 수 있는 네트워크 항목

|점검 항목|가능 여부|사용 가능한 Exporter|
|---|---|---|
|**CPU 사용률 (라우터, 스위치 등 네트워크 장비)**|✅ 가능|`snmp_exporter`|
|**메모리 사용률 (라우터, 스위치 등 네트워크 장비)**|✅ 가능|`snmp_exporter`|
|**네트워크 인터페이스 사용률 (네트워크 병목 확인)**|✅ 가능|`node_exporter`, `snmp_exporter`|
|**인터페이스/모듈 상태 (Down/Up, CRC Error 증가 여부)**|✅ 가능|`snmp_exporter`|
|**VLAN 상태 및 Tagging 확인**|✅ 가능|`snmp_exporter` (VLAN 정보 수집 가능)|
|**LB 상태 확인 (부하 분산 및 Health-Check 상태 점검)**|✅ 가능|`blackbox_exporter`, `haproxy_exporter`|
|**Mac/ARP Table 상태 확인**|✅ 가능|`snmp_exporter`|
|**라우팅 Table 상태 확인 (Static/OSPF/BGP)**|✅ 가능|`snmp_exporter`|
|**STP 상태 점검 (Loop 방지 및 통신 상태 확인)**|✅ 가능|`snmp_exporter`|
|**이중화 구성 상태 점검 (Failover 상태 확인)**|✅ 가능|`snmp_exporter`|
|**통신 테스트 (특정 장비와의 연결 확인)**|✅ 가능|`blackbox_exporter` (ICMP Ping, TCP/HTTP 체크)|
|**HW 상태 관련 로그 점검 (Fail, Error, Warning 등)**|✅ 가능|`promtail` + `Loki`|

---

### 📌 세부 설명

1. **자원 사용률 점검 (CPU, 메모리, 네트워크 인터페이스)**
    
    - `snmp_exporter`를 활용하여 라우터, 스위치 등의 CPU 및 메모리 사용률을 모니터링 가능.
    - `node_exporter` 또는 `snmp_exporter`를 활용하여 네트워크 인터페이스 사용률을 확인 가능.
2. **인터페이스/모듈 상태 점검**
    
    - `snmp_exporter`에서 각 포트별 상태(Up/Down) 및 CRC 오류 증가 여부를 수집 가능.
    - VLAN 정보를 확인할 수도 있으며, 필요하면 스위치별 VLAN 태깅 상태를 추적 가능.
3. **서비스 상태 점검**
    
    - 부하 분산(LB) 상태 확인
        - `haproxy_exporter`를 활용하여 HAProxy 기반 로드밸런서 상태를 확인 가능.
        - `blackbox_exporter`를 활용하여 특정 서버의 Health Check 수행 가능.
    - Mac/ARP 테이블 상태 확인
        - `snmp_exporter`에서 Mac/ARP 테이블을 모니터링 가능.
    - 라우팅 테이블 상태 확인
        - `snmp_exporter`에서 Static/OSPF/BGP 등의 라우팅 테이블 정보를 수집 가능.
    - STP 상태 점검
        - `snmp_exporter`에서 STP 설정 상태 및 Loop 발생 여부를 확인 가능.
    - 이중화 상태 점검 (Failover)
        - `snmp_exporter`에서 장비의 HA (High Availability) 상태를 모니터링 가능.
    - 특정 장비와의 통신 상태 확인
        - `blackbox_exporter`를 사용하여 Ping(ICMP), TCP, HTTP(S) 기반의 연결 상태를 점검 가능.
4. **로그 점검**
    
    - `promtail` + `Loki`를 활용하여 네트워크 장비의 로그(Fail, Error, Warning 등)를 수집하여 알람 설정 가능.

---

### ❌ Prometheus로 직접 확인하기 어려운 항목

- VLAN 태깅 상태가 잘못 설정된 경우, Prometheus에서 직접 탐지하기 어려움.
    - 수집된 SNMP 데이터를 기반으로 분석 스크립트가 필요할 수 있음.

---

### 🔥 결론

- `snmp_exporter`, `blackbox_exporter`, `haproxy_exporter`, `promtail + Loki` 등을 활용하면 대부분의 네트워크 모니터링이 가능함.
- 다만, VLAN 태깅 오류 등의 복잡한 네트워크 설정 검증은 Prometheus에서 직접 감지하기 어려울 수 있음.