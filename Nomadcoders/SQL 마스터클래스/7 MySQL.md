## #7.0 Introduction 

## #7.1 Installation

## #7.2 MySQLWorkbench

## #7.3 Connecting

## #7.4 MySQL Data Types Part One

## #7.5 MySQL Data Types Part Two

```sql
create table users (
    user_id bigint unsigned primary key auto_increment,
    username char(10) not null unique, -- 'nico' --> 'nico      '
    email varchar(50) not null, -- 'nico@nomad.co' --> 'nico@nomad.co'
    gender enum ('Male', 'Female') not null,
    interests set (
        'Technology',
        'Sports',
        'Music',
        'Art',
        'Travel',
        'Food',
        'Fashion',
        'Science'
        ) not null,
    bio text not null, -- tinytext 255, text 64kb, mediumtext 16mb, longtext 4gb
    profile_picture tinyblob, -- tinyblob, blob, mediumblob, longblob
    /*
      -- tinyint
      -- signed: -128 to 127
      -- unsigned: 0 to 255

      -- smallint
      -- signed: -32,768 to 32,767
      -- unsigned: 0 to 65,535

      -- mediumint
      -- signed: -8,388,608 to 8,388,607
      -- unsigned: 0 to 16,777,215

      -- int
      -- signed: -2,147,483,648 to 2,147,483,647
      -- unsigned: 0 to 4,294,967,295

      -- bigint
      -- signed: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
      -- unsigned: 0 to 18,446,744,073,709,551,615
     */
    age tinyint unsigned not null,
    is_admin boolean default false not null, -- tinyint(1,0)
    balance float default 0.0 not null, -- decimal(precision, scale) float 1.40
    /*
     timestamp -> '1970-01-01 00:00:01' UTC to '2038-01-19 03:14:07' UTC
     datetime -> '1000-01-01 00:00:00' to '9999-12-31 23:59:59'
     */
    joined_at timestamp default current_timestamp not null , -- datatime yyyy-mm-dd hh:mm:ss
    updated_at timestamp default current_timestamp on update current_timestamp not null,
    birth_date date not null,
    bed_time time not null ,
    graduation_year year not null, -- 1901 to 2155
    -- JSON, GE9OMETRY, POINT, LINESTRING, POLYGON, MULTIPOINT, MULTILINESTRING, EMULTIPOLYGON & GEOMETRYCOLLECTION

    constraint chk_age check(age < 100),
    constraint uq_email unique (email)
);
```

## #7.6 INSERT INTO VALUES

## #7.7 ALTER TABLE