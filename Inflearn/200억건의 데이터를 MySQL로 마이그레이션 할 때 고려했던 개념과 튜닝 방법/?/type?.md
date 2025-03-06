
# EXPLAN - `type` column

### system
- 단 하나의 행(row)만 있는 테이블에 대한 조회.
- 가장 빠른 방식
### const
- 프라이머리 키(PK) 또는 유니크 인덱스(UNIQUE INDEX)로 WHERE 절에서 특정 값을 조회할 때 사용
- 최대 1건만 반환
### eq_ref
- 조인에서 프라이머리 키(PK) 또는 유니크 인덱스(UNIQUE)를 사용하여 정확히 1개의 행을 조회
- 일반적으로 `= (equal)`비교 연산자가 사용될 때 나타난다.
### ref
- 일반적인 인덱스를 사용한 조회
- 여러 개의 행을 반환할 수도 있다.
- `=` or `IN`연산자가 WHERE 조건에서 사용될 때 등장
### fulltext
- `FULLTEXT`인덱스를 이용한 검색
### ref_or_null
- `ref`와 비슷하지만, `NULL`값을 포함하는 경우도 검색
### index_merge
- 여러 개의 인덱스를 조합해서 검색.
### unique_subquery
- `IN (SELECT ...)`형태의 서브쿼리에서 유니크 인덱스를 활용하는 경우
### index_subquery
- `IN (SELECT ...)`서브쿼리에서 일반 인덱스를 활용하는 경우
### range
- 인덱스를 사용하지만 특정 범위를 조회 (`BETWEEN`, `>`, `<`, `IN`, `LIKE ‘%’` 등)
### index
- 테이블의 모든 인덱스를 스캔
- `WHERE`절 없이 인덱스 순서대로 데이터를 읽을 때 발생
### ALL
- 테이블 전체를 스캔(Full Table Scan)
- 가장 비효율적이며, WHERE 조건에 인덱스를 활용하지 못할 때 발생

