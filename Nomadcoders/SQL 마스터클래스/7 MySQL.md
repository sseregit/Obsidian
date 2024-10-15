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
```sql
-- drop column
alter table users drop column profile_picture;

-- rename column
alter table users change column about_me about_me text;

-- change the column type
alter table users modify column about_me tinytext;

-- rename database
alter table users rename to customers;

alter table customers rename to users;

-- drop constraints
alter table users drop constraint uq_email;
alter table users drop constraint username, drop constraint chk_age;

-- adding constraints
alter table users add constraint uq_email unique (email), add constraint uq_username unique (username);

alter table users add constraint chk_age CHECK (age < 100);

alter table users modify column bed_time time null;
alter table users modify column bed_time time not null;

show create table users;
```

## #7.8 ALTER TABLE part Two

sqlite는 `alter table`을 지원하지만 테이블 이름 변경, 컬럼 추가, 컬럼 이름 변경 밖에 할 수 없다.

### 데이터를 가지고 있는 컬럼의 타입을 변경할 때 방법
1. 완전히 새로운 컬럼을 만든다.
	1. 새로운 컬럼을 만들시 not null을 지정하면 반드시 default 값이 있어야 한다
	2. 새로운 컬럼에 타겟 컬럼을 migrationd을 진행한다.
	3. 그후 타겟 컬럼 삭제
2. 완전히 새로운 컬럼을 만들면서 Default 로 해당 값을 채운뒤 삭제할 수 있다.

## #7.9 Generated Columns

### Computed Column (Generated Column)
- 다른 컬럼을 사용하여 값을 도출하는 컬럼
- stored
	- `full_name varchar(101) generated always as (concat(first_name, ' ', last_name)) stored`
	- 디스크에 저장된다.
	- 업데이트 될때만 다시 계산된다.
- virtual
	- `alter table users_v2 add column email_domain varchar(50) generated always as (substring_index(email, '@', -1)) virtual;`
	- 디스크나 데이터베이스에 저장되지 않는다.
	- 조회할 때마다 매번 연산을 수행한다