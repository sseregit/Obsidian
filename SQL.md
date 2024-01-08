
## Window 절 구문
- ROWS | RANGE
	- ROWS
		- 물리적인 row
	- RANGE
		- 논리적인 row
	- **Order by** 절이 없으면 해당 구문은 기술 할 수 없다.
- BETWEEN
	- 시작 지점
	- UNBOUNDED PRECEDING
		- Partition의 첫번째 row부터 시작 종료점으로 사용 불가능.
	- CURRENT ROW
		- 시작점또는 종료점으로 사용될 수 있으나, 보통은 **종료점으로 사용**
	- value_expr
		- PRECEDING
		- FOLLOWING
- AND
	-  종료지점
	- UNBOUNDED FOLLOWING
		- 마지막 row에서 종료됨 시작점으로 사용 불가능.
	- CURRENT ROW
	- value_expr {PRECEDING | FOLLOWING}
	- UNBOUNDED PRECEDING | CURRENT ROW | value_expr PRECEDING

- ROWS + value 표현 PRECEDING *or* value 표현 FOLLOWING
	- 특정한 지점을 window의 시작 또는 종료 지점 으로 나타낼수 있다.
- RANGE + value 표현 PRECEDING *or* value 표현 FOLLOWING
	- 단순한 숫자외에도 논리적인 값을 적용해야함 **interval값**이 사용됨
	- Order by 절의 컬럼도 numberic 또는 (대부분) date/timestamp가 되어야 한다.

- Window 절에 between이 주어지지 않고 시작 범위만 주어질 때 종료범위는 자동으로 current row가 된다.

