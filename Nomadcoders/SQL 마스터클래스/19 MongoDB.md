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

### [query operator](https://www.mongodb.com/ko-kr/docs/manual/reference/operator/query/)

```mongo
db.movies.find();  
  
db.movies.find({director: "Christopher Nolan"});  
  
db.movies.find({rating: {$gte: 8}});  
  
db.movies.find({year: {$gt: 2000, $lt: 2005}});  
  
db.movies.find({$or: [{rating: {$gt: 9}}, {year: {$gte: 2005}}]})  
  
db.movies.find({genres: {$in: ["Drama", "Crime"]}});  
  
db.movies.find({genres: {$all: ["Drama", "Crime"]}});  
  
db.movies.find({title: {$regex: /the/i}});  
  
db.movies.find({genres: {$size: 3}});  
  
db.movies.find({director: {$exists: false}});  
  
db.movies.find({"cast.0": "Keanu Reeves"});  
  
db.movies.find().sort({rating: -1, title: 1}).limit(10).skip(10) // 1 오름차순, -1 내림차순
```

## #19.4 Updating Documents

```mongodb
db.movies.updateOne(  
    {_id: ObjectId('6711c501aaca8d2c1319f4ae')},  
    {  
        $set: {'director': 'Francing Ford Coppola'},  
        $currentDate: {updated_at: true}  
    }  
);  
  
db.movies.findOneAndUpdate(  
    {_id: ObjectId('6711c501aaca8d2c1319f4ae')},  
    {  
        $set: {'director': 'Francing Ford Coppola'},  
        $currentDate: {updated_at: true}  
    },  
    {  
        returnNewDocument: true,  
        upsert: true  
    }  
);  
  
db.movies.updateMany({  
    director: 'Christopher Nolan'  
}, {  
    $inc: {rating: 0.2}  
});  
  
db.movies.updateMany({  
    title: 'Inception'  
}, {  
    $push: {genres: "Mind-Control"}  
});  
  
db.movies.updateMany({  
    title: 'Inception'  
}, {  
    $pull: {genres: "Mind-Control"}  
});  
  
db.movies.updateMany({  
    title: 'The Dark Knight'  
}, {  
    $addToSet: {cast: "Michael Cane!"}  
});  
  
db.movies.updateMany({}, {  
    $rename: {runtime: 'duration'}  
});  
  
db.movies.updateOne(  
    {title: "Inception"},  
    {  
        $set: {  
            boxOffice: {  
                domestic: 292352352,  
                international: 235235235,  
                worldwideTotal: 315235235  
            }  
        }  
    }  
)  
  
db.movies.updateOne(  
    {title: "Inception"},  
    {$set: {"domestic": ""}}  
)  
  
db.movies.updateMany(  
    {},  
    {$unset: {"international": "", "worldwideTotal" : ""}}  
)  
  
db.movies.updateMany(  
    {$expr: {$lt: [{$size: "$genres"}, 3]}},  
    { $addToSet: { genres: { $each: ["Other", "Happy"]}}}  
)  
  
db.movies.deleteMany({})  
  
db.movies.find();
```

## #19.5 Aggregating Documents

### [Aggregation](https://www.mongodb.com/ko-kr/docs/manual/aggregation/)
