### **📋 1.1.1 서버 점검 항목 및 Prometheus 사용 가능 여부**

|**번호**|**점검 항목**|**Prometheus 사용 가능 여부**|**사용할 Exporter**|
|---|---|---|---|
|**① CPU**||||
|①-1|CPU 사용률|✅ 가능|`node_exporter`|
|①-2|CPU 코어별 상태 점검|✅ 가능|`node_exporter`|
|**② MEMORY**||||
|②-1|메모리 사용률|✅ 가능|`node_exporter`|
|②-2|메모리 상태 확인 (할당된 메모리 정상 인식 여부 확인)|✅ 가능|`node_exporter`|
|②-3|Paging Space 사용률 (가상 메모리 사용 가능 여부 확인)|✅ 가능|`node_exporter`|
|**③ DISK**||||
|③-1|파일시스템 사용량 점검|✅ 가능|`node_exporter`|
|③-2|Disk Swap 사용률 (가상 메모리 사용 가능 여부 확인)|✅ 가능|`node_exporter`|
|③-3|Disk 이중화 정상 여부 (RAID 구성 및 상태 확인)|✅ 가능 (RAID 환경)|`node_exporter` (RAID 관련 메트릭 제공)|
|③-4|Disk 인식 여부 점검 (Disk Status: Unknown/Drive not available 감지)|❌ 불가능|OS 명령어 필요 (`lsblk`, `fdisk -l`)|
|③-5|Disk I/O 점검 (Soft Errors, Hard Errors, Transport Errors, Iowait 지연 확인)|✅ 부분 가능|`node_exporter` (I/O 성능 측정 가능, Soft/Hard Errors는 불가능)|
|③-6|I-Node 사용률 점검 (파일시스템의 I-Node 사용량 분석)|✅ 가능|`node_exporter`|
|**④ KERNEL**||||
|④-1|Kernel Parameter Check (커널 설정값 점검 및 OS 장애 예방)|✅ 부분 가능|`node_exporter` (파일 핸들, 메모리 설정 모니터링 가능, `sysctl` 값 직접 확인 불가)|
|**⑤ 시스템 로그 및 성능 점검**||||
|⑤-1|시스템 로그 (장치 및 인스턴스 성능 저하 또는 손실 우려 확인)|✅ 부분 가능|`node_exporter` (CPU, 메모리, 디스크 사용량 모니터링 가능, 로그 분석은 불가능)|
|**⑥ 클러스터 및 공유 볼륨**||||
|⑥-1|Cluster 데몬 상태 점검 (클러스터 정상 운영 여부 확인, Maintenance/Offline 감지)|✅ 부분 가능|`kube-state-metrics` (Kubernetes 환경) / `pacemaker_exporter` (Pacemaker 환경)|
|⑥-2|공유 볼륨 상태 점검 (Read/Write 상태 및 마운트 정상 여부 확인)|✅ 부분 가능|`node_exporter` (마운트 상태 확인 가능), `gluster_exporter` (GlusterFS 환경)|