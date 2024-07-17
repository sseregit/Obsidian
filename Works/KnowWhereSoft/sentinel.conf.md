```conf
# Sentinel 기본 설정
# 해당 master를 모니터링하라고 알리는데 사용한다
sentinel monitor <master-name> <master-ip> <master-port> <quorum>
sentinel auth-pass <master-name> your-redis-password
# 다운된 것으로 간주하기 시작하기 전까지 인스턴스에 연결 할수 없어야 하는 시간(밀리초)
sentinel down-after-milliseconds <master-name> 5000
# 장애 조치후 새 마스터를 사용하도록 동시에 재구성할 수 있는 복제본의 수를 설정
sentinel parallel-syncs <master-name> 1
# 장애 조치가 일정 시간이 지나도 완료되지 않았으면 취소 하는 시간
sentinel failover-timeout <master-name> 60000
# Sentinel 이벤트가 발생할 때 알림을 받을 수 있도록 스크립트를 설정합니다.
sentinel notification-script <master-name> /path/to/notify.sh
# 마스터가 변경될 때 클라이언트 재구성을 위한 스크립트를 설정합니다.
sentinel client-reconfig-script <master-name> /path/to/reconfig.sh
# Sentinel 노드 간 통신을 보호하기 위해 패스워드를 설정합니다.
sentinel auth-pass <master-name> your-redis-password
```