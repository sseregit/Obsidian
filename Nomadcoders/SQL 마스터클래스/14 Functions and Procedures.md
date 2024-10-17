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