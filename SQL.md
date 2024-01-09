
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

## range와 rows 적용 시 유의 사항
- 집계 계열 analytic 함수는 order by 절이 있을 경우 window 절은 기본적으로 **range between unbounded preceding and current row**이다.
	- **range를 적용할 경우 order by에서 동일 값이 있을 경우**
		- current row를 자신의 row가 아닌 동일 값이 있는 전체 row를 동일 그룹으로 간주하여 집계 analytic을 적용하므로 **rows를 명시적으로 사용하는 경우와 값이 달라질 수 있음.**

## LAG() 와 LEAD() Analytic SQL
- LAG
	- 현재 행 보다 이전 행의 값을 가져온다.
- LEAD
	- 현재 행보다 다음 행의 값을 가져온다.
```
LAG(expr [,offset] [,default]) OVER([partition_by_clause]) order_by_claues)

LEAD(expr [,offset] [,default]) OVER([partition_by_clause]) order_by_claues)
```
- expr
	- 적용할 컬럼명
- offset
	- 값을 가져올 행의 위치 offset값 기본값 1
- default
	- 행의 위치 offset으로 Null값 일 때 대체할 값. 기본값은 Null
	- offset이 1이라더라도 함께 작성해야함.
- partition by는 생략 가능하지만, **order by 는 반드시 필요하다**
- **window절은 사용되지 않는다.**

## first_value() 와 last_value() Analytic SQL
- window에서 order by로 기술된 순으로 가장 첫번째/가장 마지막에 **위치**한 데이터를 가져온다.
	- 값에 대한 first와 last가 아니다.
- partition by는 생략 가능하지만, **order by는 반드시 필요하다**
- window절은 생략 가능 생략 시 range between unbounded preceding and current row

## 순위 함수
- cume_dist()
	- 분위수를 파티션내의 건수로 적용 0 ~ 1 사이 값으로 변환
- percent_rank()
	- Rank()를 0 ~ 1 사이 값으로 정규화 시킴
- ntile
	- 지정된 숫자만큼의 분위를 정하여 그룹핑하는데 적용