
[hibernate 6.0 migration guide Query](https://docs.jboss.org/hibernate/orm/6.0/migration-guide/migration-guide.html#query)
[bulk_id_strategy](https://in.relation.to/2017/02/01/non-temporary-table-bulk-id-strategies/)
[# PostgreSQL schema 의미 및 권한관리](https://kimdubi.github.io/postgresql/pg_schema/)

- application.properties, application.yml의 spring.jpa.properties.* 의 **모든 속성은 EntityManagerFactory로 전달된다.**

- 변경에 있어서 가장 큰 변화
	- 전략 전환
		- 임시 테이블 사용(기본값
		- 🔽
		- CTE에서 DML 사용(DB2 및 PostgreSQL에서 사용됨)
	- postgresql
		- database와 schema의 관련 ddl-auto : create로 적용시 내가 원하는 schema로 테이블을 등록할수 있는지..?

- 전략전환은 Dialect에 따라 적용된다
- 내가 만약에 전략을 바꿀려면 먼저 
