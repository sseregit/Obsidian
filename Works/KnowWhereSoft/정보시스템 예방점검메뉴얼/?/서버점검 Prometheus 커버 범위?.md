다음은 **Linux 환경에서 Prometheus를 활용하여 점검할 수 있는 항목과 불가능한 항목을 모두 포함한 표**입니다.  
각 항목별로 **Prometheus를 통해 점검이 가능한지 여부와, 가능하다면 어떤 Exporter를 사용할 수 있는지**를 정리하였습니다.

---

### **📋 1.1.1 서버 점검 리스트 (Linux 기준, Prometheus 활용 가능 여부 포함)**

|**구분**|**세부 점검 항목**|**설명**|**Prometheus 사용 가능 여부**|**사용할 Exporter**|
|---|---|---|---|---|
|**① CPU**|①-1 CPU 사용률|CPU 사용률 점검|✅ 가능|`node_exporter`|
||①-2 CPU 코어별 상태 점검|물리적 코어의 정상(online/offline) 유무 점검|✅ 가능|`node_exporter`|
|**② MEMORY**|②-1 메모리 사용률|메모리 사용량 점검|✅ 가능|`node_exporter`|
||②-2 메모리 상태 확인|할당된 메모리가 정상적으로 인식되고 있는지 점검|✅ 가능|`node_exporter`|
||②-3 Paging Space 사용률|가상 메모리 사용 가능 여부 확인|✅ 가능|`node_exporter`|
|**③ DISK**|③-1 파일시스템 사용량|파일시스템 사용량 점검|✅ 가능|`node_exporter`|
||③-2 Disk Swap 사용률|가상 메모리 사용 가능 여부 확인|✅ 가능|`node_exporter`|
||③-3 Disk 이중화 정상 여부|RAID 구성 및 상태 점검|✅ 가능 (RAID 환경)|`node_exporter` (RAID 관련 메트릭 제공)|
||③-4 Disk 인식 여부 점검|Disk Status: Unknown/Drive not available 감지|❌ 불가능|OS 명령어 필요 (`lsblk`, `fdisk -l`)|
||③-5 Disk I/O 점검|Iowait, I/O 지연 확인|✅ 가능|`node_exporter`|
||③-6 I-Node 사용률|파일시스템의 I-Node 사용량 분석|✅ 가능|`node_exporter`|
|**④ KERNEL**|④-1 Kernel Parameter Check|커널 설정값 점검 (파일 핸들, 메모리 설정)|✅ 부분 가능|`node_exporter` (sysctl 값 직접 확인 불가)|
|**⑤ 시스템 로그 및 성능 점검**|⑤-1 시스템 로그 점검|장치 및 인스턴스의 성능 저하 또는 손실 우려 확인|❌ 불가능|OS 명령어 필요 (`dmesg`, `/var/log/messages` 분석)|
|**⑥ 클러스터 및 공유 볼륨**|⑥-1 Cluster 데몬 상태 점검|클러스터 정상 운영 여부 확인 (Maintenance/Offline 감지)|✅ 가능 (Kubernetes)|`kube-state-metrics`, `pacemaker_exporter`|
||⑥-2 공유 볼륨 상태 점검|NFS, GlusterFS 마운트 및 Read/Write 상태 점검|✅ 가능|`node_exporter`, `gluster_exporter`|
|**⑦ NETWORK**|⑦-1 NW 링크 상태 점검|Network 인터페이스 연결상태 점검|✅ 가능|`node_exporter`|
||⑦-2 NIC 이중화 점검|Bonding 상태 확인|✅ 가능|`node_exporter`|
||⑦-3 Ping Loss 점검|네트워크 통신 상태 점검|✅ 가능|`blackbox_exporter`|
|**⑧ OS**|⑧-1 Path 이중화 점검|Multipath 이중화 정상 유무 점검|✅ 부분 가능|`node_exporter` (Multipath 전용 메트릭 부족)|
||⑧-2 HBA 연결 상태 점검|HBA 연결 정상 유무 점검 (State Online, Current Speed)|❌ 불가능|OS 명령어 필요 (`sanlun fcp show adapter`, `fcinfo hba-port`)|

---

### **📌 설명**

- ✅ **가능:** Prometheus 및 해당 Exporter를 사용하여 점검 가능.
- ✅ **부분 가능:** 일부 항목을 모니터링할 수 있으나, 추가적인 설정 또는 외부 도구 필요.
- ❌ **불가능:** Prometheus에서 직접 점검할 수 없음. OS 명령어나 추가적인 모니터링 솔루션 필요.

---

### **🔹 결론**

✅ **Linux 환경에서 `node_exporter`, `blackbox_exporter`, `kube-state-metrics` 등을 활용하여 대부분의 서버 점검 가능**  
✅ **CPU, 메모리, 디스크, 네트워크, 클러스터 관련 상태를 Prometheus 기반으로 모니터링 가능**  
❌ **Disk 인식 여부, OS 로그 분석, HBA 상태 점검 등은 Prometheus에서 직접 확인 불가 (OS 명령어나 추가 도구 필요)**

이 정보를 기반으로 **Prometheus 기반의 Linux 서버 모니터링을 구성할 수 있습니다**.  
필요하면 **Grafana 대시보드 설정이나 PromQL 쿼리**도 추가로 제공해드릴 수 있어요! 🚀😊