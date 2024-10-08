## #3.0 Introduction\
- DDL
	- 데이터베이스가 어떠한 데이를 가질지 정의하는 명령어에만 집중한다

## #3.1 Tables

## #3.2 CREATE TABLE
```sql
CREATE TABLE movies (  
    title,  
    released,  
    overview,  
    rating,  
    director  
);
```
- sqlite를 사용하기 때문에 가능한 문법

## #3.3 INSERT INTO VALUES
```sql
INSERT INTO movies
VALUES (
        'The Godfather',
        1980,
        'The best movie in the world',
        10,
        'F.F.C'
       );
```

## #3.4 INSERT INTO VALUES part Two

## #3.5 Data Types