## #12.0 Introduction
### Full-Text Index
- LIKE만으로는 할 수 없는 것을 가능하게 해준다.

## #12.1 Natural Language Search

`create fulltext index idx_overviwe on movies (overview);`

Text Field 전체 내용을 indexing한다.

### Natural Langage FullText Search
```sql
select title, overview, match(overview) against ('the food and the drinks') as score
from movies
where match(overview) against ('the food and the drinks');
;
```

[불용어는 Query에서 제거 된다](https://dev.mysql.com/doc/refman/8.4/en/fulltext-stopwords.html)

## #12.2 Boolean Mode Search

### [Boolean Mode](https://dev.mysql.com/doc/refman/8.4/en/fulltext-boolean.html)
- Boolean 로직을 사용해서 검색할 수 있다.

```sql
-- + 반드시 포함
-- - 반드시 없어야함
-- > 있는게 더 좋고
-- < 없는게 더 좋다
-- 아무 연산자도 없으면 있어도 없어도 상관없다
-- 공백이 포함되어 있다면 ""로 감싸야 한다
-- () 공백을 기준으로 여러 단어 추가 가능
-- 단어* 단어로 시작하는 단어가 있는것을 찾는다
select title, overview, match(overview) against ('psycho*' IN BOOLEAN MODE) as score
from movies
where match(overview) against ('psycho*' IN BOOLEAN MODE);
;
```

## #12.3 Query Expansion

### Query Expansion Search
- 해당 단어를 입력하면 쿼리와 관련 있는 결과를 찾고
- 그 결과에서 연관성 높은 단어를 찾아서 다시 검색한다.
	- 입력한 단어와의 연관성
		- ex) database 입력
			- MYSQL, ORACLE, DB2, RDBMS등의 연관된 단어까지 찾는다.