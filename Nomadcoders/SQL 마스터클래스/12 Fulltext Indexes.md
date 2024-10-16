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