# 1. 시스템 단위 락
## 글로벌 락(Global Lock)
- 서버 전체에 영향을 주는 락
- `FLUSH TABLES WITH READ LOCK`
- 백업 시 주로 사용
# 2. 테이블 단위락
## 테이블 락(Table Lock)
- `LOCK TABLES` 명령으로 설정
- `READ`와 `WRITE`모드 존재
- [[MyISAM?]] 스토리지 엔진에서 자주 사용
## 메타데이터 락(Metadata Lock)
- DDL(테이블 구조 변경)작업 보호
- `ALTER TABLE`, `DROP TABLE`등의 실행 시 발생
## 의도적 락(Intention Lock)
- 테이블에 잠금 의도를 표시하는 락
- `IS`(의도적 공유 락), `IX`(의도적 배타적 락) 존재
- 테이블과 레코드 락의 충돌 방지
# 3. 행(레코드) 단위 락
## 레코드 락(Record Lock)
- 특정 인덱스 레코드만 잠금
- 트랜잭션 충돌 방지
## 공유 락(Shared Lock, S-Lock)
- 여러 트랜잭션이 동시에 읽기 가능
## 배타적 락(Exclusive Lock, X-Lock)
- 쓰기 작업을 위해 하나의 트랜잭션만 접근 가능
## 넥스트 키락(Next-key Lock)
- 레코드 락 + 갭 락(범위 내 레코드와 갭을 동시에 잠금)
- [[팬텀 리드 방지?]]
## 갭 락(Gap Lock)
- 레코드 사이의 ‘공간’을 잠그는 락
- 새로운 데이터 삽입 방지([[팬텀 리드 방지?]])
## 삽입 의도 락(Insert Intention Lock)
- 동일한 갭에 여러 개의 `INSERT` 시 충돌 방지
# 4. 기타 특수 락
## 네임드 락(Named Lock)
- `GET_LOCK()`, `RELEASE_LOCK()`함수 사용
- 특정 작업을 동기화할 때 사용
## 자동 증가 락(Auto-increment lock)
- `AUTO_INCREMENT`컬럼의 값을 순차적으로 할당