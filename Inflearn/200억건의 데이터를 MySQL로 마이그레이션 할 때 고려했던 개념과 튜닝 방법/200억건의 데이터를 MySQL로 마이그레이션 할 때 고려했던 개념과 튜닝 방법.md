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
[[파일 솔트?]]


****
# 5. INSERT

****
# 6. AUTO_INCREMENT LOCK

****
# 7. Index Dive Using In Query

****
# 8. Prefix Index

****
# 9. MySQL Lock Type

****
# 10. DeadLock Case

****
# 11. NoOffset For Query Tuning

****
# 12. Skip Locked For Session

****