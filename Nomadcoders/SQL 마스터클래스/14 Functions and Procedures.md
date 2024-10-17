## #14.0 Introduction

## #14.1 Functions

### function
- 반드시 value를 return 한다.
- DML command에서 사용하기 위함이다
- 이름으로만 구별이 되지 않는다
	- 입력값, type, 순서등이 다르면 이름만 같은 펑션이 만들어 진다. 오버로딩

```sql
create or replace function hello_world(text, text)
    returns text as
$$
    select 'hello ' || $1 || ' and ' || $2;
$$
    language sql;
```

## #14.2 Return Types

## #14.3 Trigger Functions

### Function Volatility(함수 변동성)
- 기본적으로 생성할 때 코드에 작성하는건 아닌데 하지만 원하면 query 플래너가 function을 최적화 할 수 있도록 수정할 수 있다.

```sql
create or replace function set_updated_at()
    returns trigger as
    $$
		...
    $$
    language plpgsql volatile -- 이부분의 옵션 종류;
```

### volatile
- database 수정하는 것을 포함해 모든 것을 할 수 있다.
- 같은 파라미터에 다른 값이 리턴 될 수 있다.
- optimizer는 function의 작업 결과를 전혀 가정하지 않고 query가 volatile function을 사용하면 모든 각각의 row에서 재실행된다.
### stable
- 수정할 수 없는 function
- 단일 구문 내의 모든 row에서 동일한 argument에 대해서는 같은 결과를 return 한다.
- optimizer가 복수의 실행을 하나의 실행으로 최적화 해준다.

### immutable
- 수정이 불가능하다
- 동일한 argument가 주어질 경우 영원히 같은 결과를 return 한다
- query가 상수 argument와 함께 호출했다면 optimizer가 function을 미리 평가할 수 있게 해준다.

```sql
create or replace function set_updated_at()
    returns trigger as -- 이 function은 반드시 trigger에 의해 호출되어야 한다.
$$
begin
    new.updated_at = current_timestamp;
    return new;
end;
$$ language plpgsql; -- PostgreSQL이 지원하는 언어로

create trigger updated_at
    before update -- of title/ column을 target할 trigger생성가능
    on movies
    for each row
execute procedure set_updated_at();
```
### plpgsql (procedural language postgreSQL)
- trigger나 function을 작성할 때 사용할 언어

## #14.4 Procedures

### procedure
- 어떤 것도 return할 필요가 없다 할수는 있지만, 꼭 할 필요는 없음
- DML command에서 호출하지 않는다
	- `CALL (procedure name);`
- 