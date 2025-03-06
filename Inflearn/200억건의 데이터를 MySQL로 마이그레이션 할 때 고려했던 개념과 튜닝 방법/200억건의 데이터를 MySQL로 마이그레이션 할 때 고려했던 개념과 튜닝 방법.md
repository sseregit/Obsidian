# 1. 첫번째 섹션의 제목을 입력해주세요.

****
# 2. Multi Column Index
## Multi Column Index 개념
### 복합 인덱스(Multi Column Index)
```sql
CREATE TABLE ... (
	INDEX idx_col1_col2 (column1, column2) -- 복합 인덱스
)
```
- **명시된 컬럼의 순서대로 정렬이 된다.**
	- 위에 예시로 column2를 먼저 처리를 하는 Query가 들어가게 된다면 인덱스를 타지 않는다.

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