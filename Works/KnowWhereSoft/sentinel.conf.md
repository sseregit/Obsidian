```conf
# Sentinel 기본 설정
   sentinel monitor <master-name> <master-ip> <master-port> <quorum>
   sentinel auth-pass <master-name> your-redis-password
   sentinel down-after-milliseconds <master-name> 5000
   sentinel parallel-syncs <master-name> 1
   sentinel failover-timeout <master-name> 60000
# Sentinel 이벤트가 발생할 때 알림을 받을 수 있도록 스크립트를 설정합니다.
	sentinel notification-script <master-name> /path/to/notify.sh

# 마스터가 변경될 때 클라이언트 재구성을 위한 스크립트를 설정합니다.
	sentinel client-reconfig-script <master-name> /path/to/reconfig.sh
# Sentinel 노드 간 통신을 보호하기 위해 패스워드를 설정합니다.
	sentinel auth-pass <master-name> your-redis-password
```