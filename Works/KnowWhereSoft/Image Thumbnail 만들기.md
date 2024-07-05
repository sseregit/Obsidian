## [PostgreSql Text](https://www.postgresql.org/docs/current/datatype-character.html)
- Base64로 암호화된 이미지파일을 저장할때 TEXT Type의 한계는 없는가?
	- 공식 문서 기준 성능상의 차이가 없다
	- 어떤 경우든 저장할 수 있는 가장 긴 문자열은 **1GB**
- JPA에서 TEXT type을 사용하는 방법
	- [해결방법](https://rudaks.tistory.com/entry/spring-data-jpa%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%A0-%EB%95%8C-postgresql%EC%9D%98-Lob%ED%83%80%EC%9E%85-%EB%AC%B8%EC%A0%9C)
	1. `@Column(columnDefinition="TEXT")`??
	2. @Lob을 붙이면 OID(Object Identifier Types)가 들어가게 된다.
		1. Oid
			1. postgresql에서 내부 객체들을 구분하기 위해 만든 특별한 타입
		2. SELECT id, lo_get(cast(data as bigint)) 저장된 값의 변환이 일어나야 한다.

## Base64 암호화 복호화
- `java.util.Base64`
- 
## Thumbnail 라이브러리 찾기
- [생성 라이브러리 비교](https://rudaks.tistory.com/entry/%EC%8D%B8%EB%84%A4%EC%9D%BCThumbnail-%EC%83%9D%EC%84%B1-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC)
- Thumbnailator

### JSON으로 받을때 문자를 byte[] 로 받을수 있나?