## #6.0 Introduction

## #6.1 Table Scans

### Table Scan
- 데이터베이스가 무언가를 찾기 위해서 전체행을 한 행씩 찾아보는 것

## #6.2 CREATE INDEX
`create index idx_director on movies (director)`

### index
- 데이터를 저장하고 있는 데이터 구조와는 별개의 데이터 구조
- 데이터베이스가 조금 더 빠른 검색을 하기 위해 사용하는 데이터 구조

## #6.3 Disclaimer

## #6.4 B+ Trees

### internal node
- node가 달려 있는 node

### leaf node
- node가 달려 있지 않은 node

### 이동 방향
- 크면 오른쪽 작으면 왼쪽
- 검색하는 값과 비교하는 값이 같을 경우 오른쪽 이동

## #6.5 Leaf Nodes

### 왜 B+ Tree에서 꼭 Leaf node만을 찾아야 하는지
- Leaf node 안에는 (지정한 컬럼) 열의 값만이 들어 있지 않다
	- primary key값 등등이 포함
- B+ Tree에서 movies 테이블로 점프해서 movies 테이블의 정보들을 불러와야 하기 때문이다.
	- 아래 처럼 director를 index로 찾지만 title이란 값은 Leaf node에 존재 하지 않기 때문에 인덱스데이터 => 실제 데이터로 이동해야 한다.
```sql
select title from movies where director = 'blalblalblalal'
```

## #6.6 Recap

## #6.7 Indexes and Keys

## #6.8 Multi Column Indexes

### 다중 컬럼 인덱스를 만들 때는 **순서**가 중요하다
- where절에도 인덱스의 순서를 지키는것이 성능에 유리하다
- 가장 많이 사용 되는 column을 첫번째로
- DB는 범위 조건을 찾기 전까지 index 전체를 사용하려고 한다.
- = 을 우선으로 범위지정 조건 컬럼을 후순위로
범위로 지정되어 있다면 `column > 1` index의 다음 부분을 사용하지 않는다.

## #6.9 Covering Indexes

### Covering Index
- 멀티 컬럼 인덱스 만큼 드라마틱하지 않지만 훌륭한 성능 최적화를 제공한다.
- query의 요구사항을 완벽하게 만족시키는 index