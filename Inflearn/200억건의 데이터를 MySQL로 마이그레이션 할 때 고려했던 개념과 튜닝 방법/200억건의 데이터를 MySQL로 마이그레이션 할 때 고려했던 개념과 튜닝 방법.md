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
`SET optimizer_switch=“skip_scan=on” -- index skip sca`
- 일부에서 이점을 찾을 수 있다.
	- WHERE절에 조건이 없는 인덱스에 선환되는 컬럼이 유니크한 갭수가 굉장히 적어야 한다.
	- 인덱스를 타지 않아야 되는 그 필드에 대해서 나올 수 있는 컬럼의 갯수가 적어야 한다.

****
# 3. Covering Index & RDB vs ElasticSearch Index Diff

****
# 4. ORDER BY

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