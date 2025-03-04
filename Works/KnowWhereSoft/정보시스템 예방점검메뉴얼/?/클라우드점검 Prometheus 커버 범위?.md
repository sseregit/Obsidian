### ✅ Prometheus로 점검할 수 있는 가상화 및 컨테이너 환경 항목

|점검 항목|가능 여부|사용 가능한 Exporter|
|---|---|---|
|**RHEV-M (Red Hat Virtualization Manager) 가상화 SW 상태**|✅ 가능|`node_exporter`, `blackbox_exporter`|
|**하이퍼바이저 가상화 SW 상태**|✅ 가능|`node_exporter`|
|**가상화 SW 로그 (RHEV-M, 하이퍼바이저)**|✅ 가능|`promtail` + `Loki`|
|**관리 포탈 이벤트 메시지 점검**|✅ 가능|`blackbox_exporter` (API 응답 체크)|
|**하이퍼바이저 상태 점검**|✅ 가능|`node_exporter`|
|**VM(가상서버) 상태 점검**|✅ 가능|`vmware_exporter`|
|**스토리지 도메인 상태 점검**|✅ 가능|`node_exporter`, `vmware_exporter`|
|**VMWare ESXi 상태 확인**|✅ 가능|`vmware_exporter`|
|**vCenter 하이퍼바이저 점검**|✅ 가능|`vmware_exporter`|
|**vCenter와 통신하는 Agent 상태 확인**|✅ 가능|`blackbox_exporter`|
|**vSphere HA 구성 상태 확인**|✅ 가능|`vmware_exporter`|
|**VM 리스트 확인**|✅ 가능|`vmware_exporter`|
|**데이터스토어 Path 확인**|✅ 가능|`vmware_exporter`|
|**컨테이너 Worker 상태 (CPU, Memory, Storage 가용량)**|✅ 가능|`kube-state-metrics`, `node-exporter`|
|**컨테이너 POD 상태 및 로그 확인**|✅ 가능|`kube-state-metrics`, `promtail + Loki`|
|**컨테이너 시스템 로그 확인**|✅ 가능|`promtail` + `Loki`|
|**metrics-server (Autoscaling, CPU & Memory 사용량 취합)**|✅ 가능|`metrics-server`|
|**monitoring (Openshift 모니터링 - Prometheus, Grafana, Alertmanager)**|✅ 가능|`kube-prometheus-stack`|
|**node 관리 (sync pod, configmap 변경관리)**|✅ 가능|`kube-state-metrics`|
|**클러스터 네트워크 상태 점검 (SDN, OVS 상태 체크)**|✅ 가능|`kube-state-metrics`, `cilium-metrics`|
|**전체 프로젝트 누적 이벤트 로그 확인**|✅ 가능|`kube-event-exporter`|

---

### 📌 세부 설명

1. **RHEV (Red Hat Virtualization) 점검**
    
    - `node_exporter`를 활용하여 가상화 서버의 CPU, Memory, Disk 사용률 확인 가능.
    - `promtail + Loki`로 가상화 관련 로그 수집 가능.
    - `blackbox_exporter`로 RHEV 관리 포탈 API 응답 체크 가능.
2. **VMware ESXi 및 vSphere 점검**
    
    - `vmware_exporter`를 활용하여 vCenter 및 ESXi 상태 모니터링 가능.
    - `blackbox_exporter`를 사용하면 vCenter와 통신하는 Agent 정상 여부 확인 가능.
3. **컨테이너 환경 점검 (Openshift / Kubernetes)**
    
    - `kube-state-metrics`를 활용하여 각 POD의 상태 및 리소스 사용량 수집 가능.
    - `metrics-server`를 활용하여 HPA (Horizontal Pod Autoscaler) 데이터 수집 가능.
    - `promtail + Loki`로 컨테이너 관련 로그 수집 가능.
    - `cilium-metrics`를 활용하여 SDN 네트워크 상태 체크 가능.

---

### ❌ Prometheus로 직접 확인하기 어려운 항목

- 가상화 소프트웨어 내부 이벤트 및 특정 설정 값 (예: RHEV 설정 변경 여부)
- VMware vSphere 내부 정책 및 구성 (예: 특정 VM의 리소스 할당 정책)

---

### 🔥 결론

- `node_exporter`, `blackbox_exporter`, `vmware_exporter`, `kube-state-metrics`, `promtail + Loki` 등을 활용하면 가상화 및 컨테이너 환경 대부분을 모니터링 가능.
- RHEV, VMware, Openshift/Kubernetes 환경을 Prometheus로 통합 모니터링할 수 있음.