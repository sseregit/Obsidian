# 쓰기 락(Write Lock)
- 데이터를 수정하거나 삭제할 때 사용되며, 해당 데이터에 대한 배타적 접근을 보장한다.
- 쓰기 락이 설정된 데이터는 다른 트랜잭션이 읽기 또는 쓰기 작업을 수행할 수 없어 데이터 무결성을 유지한다.
## 특징
- 배타적 접근
	- 쓰기 락을 설정한 트랜잭션만이 해당 데이터에 접근하여 수정할 수 있다.
- 다른 작업 제한
	- 쓰기 락이 설정된 동안 다른 트랜잭션은 해당 데이터에 읽기 또는 쓰기 락을 설정할 수 없다.