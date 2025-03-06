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
### Prefix Index
`Alter table <테이블 명> add key (index_prefix_test(2));`
- MYSQL의 전체적인 성능을 개선할 수 있는 방법 중의 하나
- 마구잡이 사용할 수는 없다.
- 로그인 데이터를 관리하는 테이블에만 적용을 했다
	- 왜??
		- 
****
# 9. MySQL Lock Type

****
# 10. DeadLock Case

****
# 11. NoOffset For Query Tuning

****
# 12. Skip Locked For Session

****