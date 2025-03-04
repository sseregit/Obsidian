****

Prometheus를 사용하여 모니터링할 수 있는 항목과 어려운 항목을 다음과 같이 정리할 수 있습니다.  

---

## ✅ Prometheus로 점검할 수 있는 항목  

### ① CPU  
- **CPU 사용률** → `node_exporter`의 `node_cpu_seconds_total` 메트릭 활용 가능    
### ② MEMORY  
- **메모리 사용률** → `node_memory_MemTotal_bytes`, `node_memory_MemAvailable_bytes` 등을 사용해 메모리 사용률 계산 가능  
- **Paging Space 사용률** → `node_memory_SwapTotal_bytes`, `node_memory_SwapFree_bytes`를 활용하여 스왑 메모리 사용률 확인 가능  

### ③ DISK  
- **파일 시스템 사용량** → `node_filesystem_avail_bytes`, `node_filesystem_size_bytes` 활용 가능  
- **Disk I/O 점검** → `node_disk_reads_completed_total`, `node_disk_writes_completed_total`, `node_disk_io_time_seconds_total` 등을 활용 가능  
- **I-Node 사용률** → `node_filesystem_files`, `node_filesystem_files_free`를 활용하여 사용률 계산 가능  

### ④ 커널  
- **Kernel Parameter Check** → `node_exporter`의 `node_boot_time_seconds`, `node_context_switches_total`, `node_interrupts_total` 등의 커널 관련 메트릭을 참고하여 일부 점검 가능  

### ⑤ 로그  
- **로그 점검** → `promtail` 및 `Loki`와 연계하여 시스템, 커널, 메모리, I/O 에러 로그 수집 가능  

### ⑥ Cluster  
- **Cluster 데몬 상태** → 클러스터 관련 서비스가 `systemd`에서 실행 중인지 `node_systemd_unit_state` 메트릭을 통해 확인 가능  

### ⑦ Network  
- **NW 링크 상태 점검** → `node_network_up` 메트릭을 사용하여 네트워크 인터페이스 상태 확인 가능  
- **Ping Loss** → `blackbox_exporter`를 사용하여 특정 대상에 대한 `ping` 테스트 수행 가능  

---

## ❌ Prometheus로 직접 점검하기 어려운 항목  

### ① CPU  
- **물리적 코어의 Online/Offline 상태** → `lscpu` 등의 명령어로 확인해야 하며, `node_exporter`에서 직접 제공하지 않음  

### ② MEMORY  
- **메모리 상태 확인 (정상 인식 여부)** → `dmesg`나 `syslog` 등을 확인해야 하며, Prometheus 단독으로는 어렵고 `Loki`와 연계 필요  

### ③ DISK  
- **Disk Swap 사용률** → 메모리의 Swap은 가능하나 Disk 는 불가능  
- **Disk 이중화 정상 여부 (RAID 구성 및 상태 확인)** → `mdadm` 등의 툴을 사용해야 하며, Prometheus에서 기본적으로 제공하지 않음  
- **Disk 인식 여부 점검** → `lsblk` 등의 명령어를 실행해야 하며, Prometheus에서 기본적으로 제공하지 않음  

### ④ 커널  
- **커널 파라미터 설정값 점검** → `/etc/sysctl.conf` 등을 직접 확인해야 하며, Prometheus에서는 기본적으로 제공하지 않음  

### ⑤ 로그  
- **특정 이벤트 기반 로그 분석** → Loki를 사용하여 분석 가능하지만, 특정 정책을 만족하는지 자동 판단하는 기능은 부족함  

### ⑥ Cluster  
- **공유 볼륨 상태 점검** → `df -h`, `mount` 명령어를 활용해야 하며, Prometheus에서는 직접 제공하지 않음  

### ⑦ Network  
- **NIC 이중화 점검 (IPMP, Daemon 상태 확인)** → `ip link show` 또는 `ethtool` 등의 명령어로 확인해야 하며, Prometheus에서 기본 제공되지 않음  

### ⑧ OS  
- **Path 이중화 점검 (Multipath 이중화 상태 확인)** → `multipath -ll` 명령어를 실행해야 하며, Prometheus에서 직접 제공하지 않음  
- **HBA 연결 상태 점검** → `sanlun`, `fcinfo` 등의 명령어를 실행해야 하며, Prometheus에서 직접 제공하지 않음  

---

### 📌 정리  
Prometheus는 CPU, 메모리, 디스크, 네트워크 등의 성능 지표 모니터링에는 강점이 있지만, 하드웨어 이중화 상태(RAID, Multipath, HBA)나 특정 설정값(`/etc/sysctl.conf`, `mdadm`, `multipath -ll` 등`) 확인은 어렵습니다. 로그 분석 및 특정 이벤트 감지는 `Loki`와 `promtail`을 추가로 활용해야 합니다.