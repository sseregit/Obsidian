### **📋 1.1.1 서버 점검 리스트 + Prometheus 점검 가능 여부**

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
||③-5 Disk I/O 점검|Soft Errors, Hard Errors, Transport Errors, Iowait 지연 확인|✅ 부분 가능|`node_exporter` (I/O 성능 측정 가능, Soft/Hard Errors는 불가능)|
||③-6 I-Node 사용률|파일시스템의 I-Node 사용량 분석|✅ 가능|`node_exporter`|
|**④ KERNEL**|④-1 Kernel Parameter Check|커널 설정값이 기본 설정으로 유지되는지 점검|✅ 부분 가능|`node_exporter` (파일 핸들, 메모리 설정 모니터링 가능, `sysctl` 값 직접 확인 불가)|
|**⑤ 시스템 로그 및 성능 점검**|⑤-1 시스템 로그 점검|장치 및 인스턴스의 성능 저하 또는 손실 우려 확인|✅ 부분 가능|`node_exporter` (CPU, 메모리, 디스크 사용량 모니터링 가능, 로그 분석은 불가능)|
|**⑥ 클러스터 및 공유 볼륨**|⑥-1 Cluster 데몬 상태 점검|클러스터 정상 운영 여부 확인 (Maintenance/Offline 감지)|✅ 부분 가능|`kube-state-metrics` (Kubernetes 환경) / `pacemaker_exporter` (Pacemaker 환경)|
||⑥-2 공유 볼륨 상태 점검|Read/Write 상태 및 마운트 정상 여부 확인|✅ 부분 가능|`node_exporter` (마운트 상태 확인 가능), `gluster_exporter` (GlusterFS 환경)|
|**⑦ NETWORK**|⑦-1 NW 링크 상태 점검|Network 연결상태 정상 유무 점검|✅ 가능|`node_exporter`|
||⑦-2 NIC 이중화 점검|NIC 이중화(IPMP) 및 Daemon 상태 점검|✅ 가능|`node_exporter` (bonding 상태 모니터링 가능)|
||⑦-3 Ping Loss 점검|Network 통신 상태 점검 (Default Router로 Ping 테스트)|✅ 가능|`blackbox_exporter` (ICMP Ping 테스트)|
|**⑧ OS**|⑧-1 Path 이중화 점검|Multipath 이중화 정상 유무 점검|✅ 부분 가능|`node_exporter` (디스크 상태 모니터링 가능, multipath 전용 메트릭은 부족)|
||⑧-2 HBA 연결 상태 점검|HBA 연결 정상 유무 점검 (State Online, Current Speed)|❌ 불가능|OS 명령어 필요 (`sanlun fcp show adapter`)|
