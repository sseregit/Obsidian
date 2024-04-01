`spring.jpa.ddl-auto` 을 사용할 경우 @MappedSuperclass로 지정한 생성일, 수정일 등의 값을 가진 클래스의 필드들의 순서가 정상적으로 적용이 되지 않는다.

0. ddl-auto 옵션을 통해서 sequence를 생성하고 fk생성 ddl을 복사해둔다.
	1. sequnece는 이미 전략을 지정할때 이름과 옵션등을 입력하기 때문에 이렇게 생성해도 문제가 없다.
1. Intellij의 DDL추출을 통해 기본적인 DDL을 받는다.
	1. **스키마 주의!! 스키마를 지정하지 않으면 public스키마에 생성된다.**
2. PostgreSQL의 Naming Convention
	1. table 및 column을 lowercase로 저장한다.
	2. 기본적으로 snake_case는 적용되어 있으므로 모두 lowercase로 변경한다.
	3. **comment는 변경할 필요가 없고 대문자를 사용한 이유가 있을것으므로 주의 한다.**
3. 먼저 timestamp를 정리한다.
	1. [PostgreSQL의 날짜 타입](https://www.postgresql.org/docs/current/datatype-datetime.html#DATATYPE-DATETIME)
		1. Date
			1. YYYY-MM-DD
		2. Timestamp
			1. YYYY-MM-DD HH24:MI:SS
		3. Time
			1. HH24:MI:SS
		4. Interval
			1. N days HH24:MI_SS
	2. timestamp(12,6) => timestamp(6)으로 모두 변경해준다.
		1. timestamp(6)에 '6'은 뒤에 초 자릿수
		2. default now() 적용시에 의미가 없는거 같고 직접 입력할때 적용되는것으로 보인다.
	3. default sysdate => default now() or current_timestamp로 변경
	4. date(6) => timestamp(6)으로 변경
4. number => bigint로 변경
	1. [PostgreSQL Numberic Types](https://www.postgresql.org/docs/current/datatype-numeric.html#DATATYPE-NUMERIC)
5. 복사해둔 fk를 적용한다.
	1. ddl-auto에서 fk명을 이상한 문자로 적용하는데 이부분만 필요에 따라 변경하면됨.
6. 기존에 있던 데이터를 넣는다.
	1.  기존에 이미 등록되어 있던 데이터 이기 때문에 FK를 지정하기 전에 데이터를 넣고 FK를 등록하는게 더 좋은 방법일꺼 같다.
7. `spring.jpa.ddl-auto` create에서 none으로 변경했는지 확인한다.