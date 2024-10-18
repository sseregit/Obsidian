## #19.0 Introduction

## #19.1 Installation

## #19.2 Creating Documents

### Mongosh
- Mongo shell

### MongoDB
- 데이터베이스가 있고 컬렉션이 있다.
- 컬렉션은 문서를 가지고 있다.
	- 문서
		- 모든 데이터가 포함된 JSON 문서

```mongodb
show dbs; -- 모든 db를 본다.

use (db명) -- postgresql처럼 default schema 같은 느낌으로 생성 및 이동

db.createCollection("movies"); // db안에 collection 생성  
  
db.movies.insertOne({  
    title:"The godfather",  
    year: 1999,  
    director: {  
        name: "F.F.C",  
        alive: true  
    },  
    genres: ['Crime', 'Drama', 'Pizza']  
});  
  
db.movies.insertMany([{  
    title: " EEAAO"  
}, {  
    title: " The Godfather II"  
}])  
  
db.dropDatabase(); // db 삭제
```

## #19.3 Reading Documents