## #15.0 Introduction

## #15.1 Transactions Are Awesome

## #15.2 ACID

### transaction 시스템은 ACID 특성을 가져야 한다
- Atomicity (원자성)
	- All or Nothing
- Consistency (일관성)
	- 유효한 상태에서 또다른 valid 상태가 되어야 한다
- Isolation (독립성)
	- 하나의 transaction에서 실행된 변경사항이 commit이 되기 전까지는 다른 transaction에는 보이지 않아야 한다
- Durability (지속성)
	- committed가 되면 무슨일이 일어나도 변경사항들이 영구적으로 유지된다는걸 확실할수 있어야 한다.

### select문이 사실상 transaction으로 취급되는 이유
- select문 뿐만 아니라 모든 구문은 그 자체로 transaction으로 여겨진다.
	- auto commit mode

## #15.3 Savepoints

### savepoint
```sql
begin; -- start transaction

	...
	
    savepoint transfer_one;

	...
	
    rollback to savepoint transfer_one;
```

## #15.4 Read Uncommited

[transaction level](https://www.postgresql.org/docs/current/transaction-iso.html)

### transaction phenomena
1. dirty read
	1. transaction이 commit되지 않은 transaction이 작성한 데이터를 동시에 읽을 때 발생
	2. Read Uncommited 가능

## ### #15.5 Repeatable Read
### transaction phenomena
 2. nonrepeatable read
 3. phantom read
 4. serialization anomaly
