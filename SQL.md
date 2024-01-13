
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

## 역분위 함수
- percentile_disc
	- 0 ~ 1 사이의 분위수값을 입력하면 해당 분위수 값 이상인 것중에서 cume_dis 값을 가지느 값을 반환 
	- 이산 역분포함수
- percentile_cont
	- 연속 역분포함수를 기반
	- 값의 보정이 있음
- 둘다 analytic SQL이 아니라 **집계 함수** 이다.
`percentile_disc(0.25) within group (order by sal)`
- within group이 들어간다.

## 서브 쿼리
- 하나의 쿼리내에 또 다른 쿼리가 포함되어 있는 쿼리
- 메인쿼리 내에 포함되어 있는 관계
- Where절에 사용될 경우 복잡한 업무적인 조건을 직관적인 SQL로 표현하여 필터링하는데 주로 사용된다.
- 유형
	- Where절
		- 메인쿼리의 집합레벨을 변경시키지 않음
	- Select절(스칼라 서브쿼리)
	- From절(인라인 뷰)
	- group by와 having에도 적용할수 있지만 활용성이 좋지않음

### where절 주요 특징
- 서브쿼리는 메인쿼리에 where 조건으로 값을 전달하거나 메인쿼리와 연결되어 메인 쿼리의 **필터링** 작업을 수행
	- 서브쿼리 컬럼은 컬럼의 값만 메인쿼리로 전달 될 수 있으며 컬럼 자체는 메인쿼리에서 사용될 수 없음.
	- 메인쿼리의 컬럼은 서브쿼리에서 사용될 수 있음
- 서브쿼리와 메인쿼리로 연결 시 **메인쿼리의 집합 레벨이 변경되지 않음**
	- 메인 쿼리와 서브쿼리와 연결 시 서브쿼리는 연결 커럼으로 **무조건 유니한 집합, 즉 1의 집합이 되므로** 메인쿼리의 집합 레벨을 변경하지 않는다.

### 서브쿼리와 세미조인(Semi-Join)
- 서브쿼리는 메인쿼리와 연결시에 조인과 유사한 방식(Semi-Join)으로 연결될 수 있다
- 단 서브쿼리는 무조건 1의 집합으로 만들어지므로 메인쿼리 집합 레벨을 변경 시키지 않음

## 서브쿼리 활용 시 유의사항
- 서브쿼가 비상관(non-correlated) 서브쿼리인가? 상관(correlated) 서브쿼리 인가?
	- 비상관 서브쿼리
		- 서브쿼리 자체적으로 메인쿼리에 값을전달
		- `select * from table where column in (select column from table2 where number > 100)`
	- 상관 서브쿼리
		- 메인쿼리에서 서브쿼리에 연결 컬럼으로 연결한 뒤에 메인쿼리에서 값을 서브쿼리로 전달(**서브쿼리내에 메인쿼리의 연결컬럼을 가지고 있다.**)
		- `select * from table a where exists (select column from table2 b where a.column = b.column)`
- 단일 행 서브쿼리/다중 행 서브쿼리
	- 메인쿼리 - 서브쿼리 연결 연산자가 단순 비교 연산자일 경우 무조건 단일행이 나와야함.
	- 다중 행 서브쿼리 in, exists 또는 all/ any인가
- in/not in, exists/not exists 차이
	- in과 exists는 보통 결과가 같다.
	- not in과 not exists는 다를수 있음 Null처리 로직이 다름
- 서브쿼리가 단일 컬럼 또는 다중 컬럼을 반환하는가?

|             | 비상관 서브쿼리 | 상관 서브쿼리 |
| ----------- | ----------- | ---------- |
| 단일행 서브쿼리 | 비교 연산자(=,<,>,>=,<=,<>)| 비교 연산자(=,<,>,>=,<=,<>)|
| 다중행 서브쿼리 | in, not in | exists, not exists |
## 비상관 서브쿼리에서 IN 연산자 - 다중행 서브쿼리
- 여러개의 레코드를 반환하는 서브쿼리를 사용할땐 반드시 **IN** 연산자를 사용해야함
- IN 연산자는 여러개의 값이 입력될 경우 개별의 값의 조건들의 **OR** 연산이 적용된다.
- 중복값이 제거된 유니크한 값으로 입력됨

## 비상관 서브쿼리에서 IN 연산자 - 단일행 서브쿼리
- 메인 쿼리에서 단순 비교 연산자로 결과값을 받을 때 **단 한 개의 행만** 서브쿼리에서 제공해야한다.

## 상관 서브쿼리
- 상관 서브쿼리는 서브쿼리내에 메인쿼리의 연결 컬럼을 가지고 있다.
- 메인쿼리에서 서브쿼리로 연결값을 전달하는 방식

### exists 연산자 - 다중행 서브쿼리
- exists는 다중행 상관 서브쿼리에서 사용되는 대표적인 연산자
- 메인쿼리의 레코드별로 **서브쿼리의 결과가 한건이라도 존재하면** true가 되어 메인쿼리의 결과를 반환

