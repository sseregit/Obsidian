## #8.0 Introduction

## #8.1 Data Normalization

### 데이터 정규화
- 관계형 데이터베이스를 구조화하는 과정
- 장점
	- Database에서 중복되는 data를 제거할 수 있게 해준다
	- 중복되지 않으므로 데이터 수정/ 추가/ 삭제가 쉽고 빠르다
	- 데이터를 일관성 유지

## #8.2 Entities

## #8.3 Foreign Keys

```sql
create table ...(
	...
	owner_id bigint unsigned,
	constraint fk명 foreign key (onwer_id) references owners (owner_id)
)
```

## #8.4 ON DELETE

`foreign key (onwer_id) references owners (owner_id) on delete`
- CASCADE
	- 관련된 레코드가 삭제되면 그것과 연결된 다른 레코드도 삭제 된다.
- NO ACTION
- RESTRICT
- SET NULL
	- table이 삭제되면 해당 왜래키를 null로 설정한다.
	- NOT NULL 제약 확인

## #8.5 One-To-Many and One-To-One
[https://dbdiagram.io/](https://dbdiagram.io/)

## #8.6 Many-To-Many



