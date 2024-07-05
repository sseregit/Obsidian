## [PostgreSql Text](https://www.postgresql.org/docs/current/datatype-character.html)
- Base64로 암호화된 이미지파일을 저장할때 TEXT Type의 한계는 없는가?
	- 공식 문서 기준 성능상의 차이가 없다
	- 어떤 경우든 저장할 수 있는 가장 긴 문자열은 **1GB**
- JPA에서 TEXT type을 사용하는 방법
	1. `@Column(columnDefinition="TEXT")`??
	2. @Lob을 붙이면 OID(Object Identifier Types)가 들어가게 된다.
		1. Oid
			1. postgresql에서 내부 객체들을 구분하기 위해 만든 특별한 타입
		2. SELECT id, lo_get(cast(data as bigint)) 저장된 값의 변환이 일어나야 한다.
