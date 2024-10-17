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

### Repeatable Read
- repeatable read transaction이 진행중 상태에서는 commit이 된 데이터도 계속해서 이전 데이터가 보이게 된다
- 스냅샷을 찍는데 transaction이 처음 열릴때 찍는것이 아니라 non-transaction 명령문이 실행될 때 찍힌다.

### transaction phenomena
 2. nonrepeatable read
	 1. transaction이 데이터를 다시 읽으려고 할 때 발생한다.
	 2. 이미 한번 읽은 데이터가 다른 transaction에서 수정되고 commit 됐을 때
	 3. 주로 update로 발생
 3. phantom read
 4. serialization anomaly

## #15.6 Phantom Read

### transaction phenomena
 3. phantom read
	 1. row(행)집합을 반환하는 쿼리를 transaction 안에서 재실행할 때, 최근에 다른 commit된 다른 transaction에 의해서 그 결과가 이전과 다르게 변경되는 것
	 2. 주로 insert와 delete로 발생
 4. serialization anomaly

## #15.7 Locks

## #15.8 Serialization Anomaly

### transaction phenomena
4. serialization anomaly
	1.  여러 트랙잭션의 성공적인 커밋 결과가 가능한 모든 순서로 트랜잭션을 순차적으로 실행한 결과와 일치하지 않을 때 발생한다.
	2. 모든 트랜잭션이 동시에 실행했을 때와 하나씩 실행할 때가 다른 결과가 나타난다면 트랜잭션이 격리되지 않은것

## #15.9 Shared Locks
