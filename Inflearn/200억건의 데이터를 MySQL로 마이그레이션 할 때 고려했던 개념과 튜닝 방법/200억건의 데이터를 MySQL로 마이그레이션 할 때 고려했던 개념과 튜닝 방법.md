# 1. 첫번째 섹션의 제목을 입력해주세요.

****
# 2. Multi Column Index
## Multi Column Index 개념
### 복합 인덱스(Multi Column Index)
```sql
CREATE TABLE ... (
	INDEX idx_col1_col2 (column1, column2) -- 복합 인덱스
	-- INDEX idx_col1_col2 (column1, column2, column3) 
	-- index dive 상황에 많은 오버헤드 발생
)
```
- **명시된 컬럼의 순서대로 정렬이 된다.**
	- 위에 예시로 column2를 먼저 처리를 하는 Query가 들어가게 된다면 인덱스를 타지 않는다.
`EXPLAN select ... from ...`
- 확인해서 type이 `index`인것을 확인하자
- type이 `ALL`이라면 풀스캔
## Multi Column Index Type 분석
[[인덱스 스킵 스캔?]]
### 복합 인덱스를 어떻게 설정하냐?
- 보통 [[카디널리티?]]라는걸 기준으로 많이 설정한다.
`show index from test1; -- 해당 테이블의 index를 보는 Query`
****
# 3. Covering Index & RDB vs ElasticSearch Index Diff
## Covering Index & RDB vs ElasticSearch Index Diff
[[Covering Index?]]
[[클러스터형 인덱스?]]
[[색인?]]
[[역색인?]]
****
# 4. ORDER BY
## ORDER BY
[[파일 소트?]]
### ORDER BY 사용 전략
1. index 설정을 잘하기
2. `sort_buffer_size` 메모리 할당량 증가 시켜주기
3. 데이터의 타입을 한정하기.

### 꿀팁
- 스트림 값에 대해서 바로 정렬을 시작하면 정렬이 원활하게 되지 않는다.

****
# 5. INSERT
## Two types of INSERT optimization
### DB에 대한 부하를 줄일 수 있는 인설트 쿼리 방법 3가지
1. DB에 대한 Connection 줄이기
	- Bulk Write, Bulk INSERT
		- 하나의 커넥션에 여러 개의 INSERT가 담긴다.
		- values에 들어갈 수 있는 값에 대한 크기가 정해져 있다.
			- `max-allowed-packet`
2. Prepared Statement
3. 파일을 이용한 Insert
### MYSQL에서 UPDATE, INSERT의 진행 방법
1. 타겟 데이터 copy
2. 변경후 문제 없으면 commit
****
# 6. AUTO_INCREMENT LOCK
## AUTO_INCREMENT LOCK
[[인터리브?]]
`innodb_autoinc_lock_mode=0 -- 동시성 보장이 안되 성능 저하`
`innodb_autoinc_lock_mode=1 --default` 
`innodb_autoinc_lock_mode=2`
- 여러 스레드가 정말 많은 스레드가 접근 할 경우에 사용할 것
****
# 7. Index Dive Using In Query
## Index Dive Using In Query
### [[Index Dive?]]
- 일종의 버그 쿼리가 늦어지는 
****
# 8. Prefix Index
## Why Don't Use Prefix Index In Default
### [[Prefix Index?]]
`Alter table <테이블 명> add key (index_prefix_test(2));`
- MYSQL의 전체적인 성능을 개선할 수 있는 방법 중의 하나
- 마구잡이 사용할 수는 없다.
- 로그인 데이터를 관리하는 테이블에만 적용을 했다
	- 왜??
		- 보통 긴 문자열의 데이터를 저장할 때 사용한다.
			- UUID, Token, Hash...
****
# 9. MySQL Lock Type
## MySQL Lock Type
### Lock & Dead Lock
- 데이터의 정합성을 높이면서도 동시성을 높이는 장점들을 동시에 가져갈 수 있는 방법
### Shared Lock
- Row레벨에 적용 된다.
	- Row레벨
		- 말그대로 하나의 로우
- 일반적으로 Read Lock으로 활용
- Lock이 만약 걸려있다면, Row Write, Update하는 Lock은 사용이 불가능하다.
- Row에 대해서 Shared Lock이 획득이 되어 있다면, Exclusive Lock은 대기하게 된다.
- Shared Lock 여러개의 트랜잭션이 공유할 수 있다.
### Exclusive Lock
- Row레벨에 적용
- Update, Write에 사용된다.
- Shared Lock과 동시에 획득할 수 없다.
### Intention Lock
- 테이블 단위의 Lock
- 쿼리에 대해서 영향을 주지 않는다.
- 여러개의 트랜잭션에서 접근이 가능하다.
- ALTER TABLE, DROP TABLE은 대기상태에 들어갈 수 있다.

[[MYSQL이 제공하는 여러개의 Lock?]]
[[Read Lock?]]
[[Write Lock?]]
****
# 10. DeadLock Case
## DeadLock Case
### DeadLock
- 일반적으로 트랜잭션 경합이 재기적으로 계속 반복되면서 결국 트랜잭션이 실패가 되는 상황
- Lock들이 서로 경합을 하다가 서로 대기가 되어버려서 아무것도 진행이 되지 않는 상황
#### 줄이는 방법
- 복잡한 쿼리를 최대한 줄이자.
- 트랜잭션에서 여러 데이터를 수정할 때 발생하는 Lock의 순서를 지켜주자
- `ON DUPLICATE KEY UPDATE`
****
# 11. NoOffset For Query Tuning
## NoOffset For Query Tuning
### No Offset
- 오프셋을 사용하지 않고 페이지네이션을 구현
### Offset
- 일반적으로 페이지네이션에 대한 쿼리를 처리할 때 사용되는 쿼리
### MySQL의 쿼리 처리 순서
1. `WHERE` 조건 및 `JOIN`을 실행
2. `GROUP BY`
3. `DISTINCT`
4. `HAVING`
5. `ORDER BY`
6. `LIMIT`
****
# 12. Skip Locked For Session
## Skip Locked For Session
### MYSQL 7.0, 8.0
- `NO WAIT`
	- 쿼리 실행 후, Lock이 걸려있다면 대기하지 않고 바로 실패
- `Skip Locked`
	- Lock이 걸려있는 Row는 결과에 반환하지 않는다.
****