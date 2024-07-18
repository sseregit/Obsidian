```conf
# 호스트 컴퓨터에서 사용 가능한 모든 네트워크 인터페이스를 연결할 수 있다.
# ex) 127.0.0.1 ::1
bind

# 지정된 포트에서 연결을 수락한다
# TLS/SSL은 비활성화 되어 있다 적용할 때 찾아볼 것
# ex) 6379
port

# 패스워드 설정
requirepass

# Redis는 기본적으로 데몬으로 실행되지 않는다
# 데몬을 실행할 경우 지정하지 않더라도 pid 파일을 사용한다
# 지정을 원하면 pidfile (file명)을 conf에 추가한다
# ex) yes or no
daemonize 

# 로그 수준을 지정한다
# debug( 개발 / 테스트)
# notice (프로덕션에 적합한 내용)
# 그외 debug -> verbose -> notice -> warning -> nothing
loglevel

# 로그 파일 이름을 지정 (경로 포함 가능)
logfile

# DB 저장
# RDB <초> <변경사항>
# 아래 기준 900초후 1회 변경이 수행된 경우
save 900 1
save 300 10
save 60 10000

# DB를 덤프할 파일 이름
dbfilename dump.rdb

# DB 작업 디렉터리
# 파일 이름이 아닌 디렉터리 입력
dir

# replica만 따로 적어주면 된다
# replicaof <master-id> <master-port>
# 마스터가 패스워드를 사용할 경우
# masterauth <master-password>
# 마스터 사용자 구성
# masteruser <username>
# replica는 읽기 전용
# replica-read-only yes

# 최대 메모리 지정
maxmemory <bytes>
# 최대 메모리 도달시 제거할 항목을 선택하는 방식
maxmemory-policy <정책>
```