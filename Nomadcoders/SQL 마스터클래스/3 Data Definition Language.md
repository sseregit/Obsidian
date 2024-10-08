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
```sql
CREATE TABLE movies
(
    title TEXT,
    released INTEGER,
    overview TEXT,
    rating REAL,
    director TEXT,
    for_kids INTEGER -- 0 or 1
    -- poster BLOB
) STRICT;
```
- **STRICT**가 없으면 타입의 검사를 하지 않는다.

## #3.6 Constraints

## #3.7 CHECK Constraint
### CHECK Constraint
- 데이터 유효성 검사를 할 때 나만의 로직을 추가할 수 있다.

## #3.8 Recap
```sql
CREATE TABLE movies
(
    title    TEXT    NOT NULL UNIQUE,
    released INTEGER NOT NULL CHECK (released > 0),
    overview TEXT    NOT NULL CHECK (LENGTH(overview) <= 100),
    rating   REAL    NOT NULL CHECK (rating BETWEEN 0 AND 10),
    director TEXT,
    for_kids INTEGER NOT NULL DEFAULT 0  CHECK (for_kids BETWEEN 0 AND 1)
    -- poster BLOB
) STRICT;
```

## #3.9 Primary Keys