## #13.0 Introduction

## #13.1 Installation

## #13.2 pgAdmin

## #13.3 PostgreSQL Data Types

### TOAST(The Oversized-Attribute Storage Technique)
- postgres는 text를 받아 압축하는데 해당 압축한 용량이 2KB를 넘으면 다른 테이블 어딘가에 저장되고 해당 text는 그 row를 가리키는 pointer를 갖게된다

## #13.4 PostgreSQL Data Types part Two

```sql
create type gender_type as enum ('male', 'female');

create table users (

    -- 0 < char(n) varchar(n) < 10,485,760
    username char(10) not null unique,
    email varchar(50) not null unique,
    gender gender_type not null,
    interest TEXT[] not null,
    -- 1GB
    -- 2KB > 압축한 TXEXT
    bio TEXT,

    profile_photo bytea,

    /*
   -- smallint
   -- signed: -32,768 to 32,767

   -- integer
   -- signed: -2,147,483,648 to 2,147,483,647

   -- bigint
   -- signed: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807

   -- serial auto_increment가 된다.
   -- smallserial
   -- signed: 1 to 32,767

   -- serial
   -- signed: 1 to 2,147,483,647

   -- bigserial
   -- signed: 1 to 9,223,372,036,854,775,807

   -- decimal & numeric(precision, scale) 10.53 4p 2s
   -- real (6 decimal digits) & double percision (15 decimal digits)
  */
    age smallint not null check (age > 0),

    is_admin boolean not null default false,

    joined_at timestamptz default current_timestamp not null,

    updated_at timestamptz default current_timestamp not null,

    birth_date date not null,
    bed_titme time not null,
    graduation_year integer not null check (graduation_year between 1901 and 2115),

    intership_period interval
)
```