# 읽기 락(Read Lock)
- 데이터를 읽는 동안 데이터의 일관성을 보장하기 위해 사용된다.
- 읽기 락이 설정된 데이터는 다른 트랜잭션이 동시에 읽을 수 있지만, 쓰기 작업은 제한된다.
## 특징
- 동시 읽기 허용
	- 여러 트랜잭션이 동시에 동일한 데이터에 읽기 락을 설정하고 조회할 수 있다.
- 쓰기 제한
	- 읽기 락이 설정된 데이터에 대해 다른 트랜잭션은 쓰기 락을 설정할 수 없어 데이터 수정이 제한된다.