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

### Volatility
- 같은 파라미터 다른 값을 리턴할 수 있다.
### Stable
- 같은 파라미터 같은 값을 리턴한다.

### Immutable
- 동일한 argument가 주어질 경우 영원히 같은 결과를 리턴