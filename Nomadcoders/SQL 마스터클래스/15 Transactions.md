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