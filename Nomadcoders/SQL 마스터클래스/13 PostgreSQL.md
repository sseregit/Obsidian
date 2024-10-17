## #13.0 Introduction

## #13.1 Installation

## #13.2 pgAdmin

## #13.3 PostgreSQL Data Types

### TOAST(The Oversized-Attribute Storage Technique)
- postgres는 text를 받아 압축하는데 해당 압축한 용량이 2KB를 넘으면 다른 테이블 어딘가에 저장되고 해당 text는 그 row를 가리키는 pointer를 갖게된다

## #13.4 PostgreSQL Data Types part Two

## #13.5 Type Casting

## #13.6 Data Import

## #13.7 UNNEST

```sql
create table genres
(
    genre_id   bigint primary key generated always as IDENTITY,
    name       varchar(50) unique,
    created_at timestamptz default current_timestamp not null,
    updated_at timestamptz default current_timestamp not null
);

insert into genres (name)
select distinct unnest(string_to_array(genres, ','))
from movies
group by genres
;

create table movies_genres
(
    movie_id   bigint                                not null,
    genre_id   bigint                                not null,
    created_at timestamptz default current_timestamp not null,
    updated_at timestamptz default current_timestamp not null,

    primary key (movie_id, genre_id),
    foreign key (movie_id) references movies (movie_id),
    foreign key (genre_id) references genres (genre_id)
);
```

## #13.8 FULL OUTER JOIN