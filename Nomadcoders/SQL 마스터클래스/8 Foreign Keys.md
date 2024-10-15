## #8.0 Introduction

## #8.1 Data Normalization

### 데이터 정규화
- 관계형 데이터베이스를 구조화하는 과정
- 장점
	- Database에서 중복되는 data를 제거할 수 있게 해준다
	- 중복되지 않으므로 데이터 수정/ 추가/ 삭제가 쉽고 빠르다
	- 데이터를 일관성 유지

## #8.2 Entities

## #8.3 Foreign Keys

```sql
create table ...(
	...
	owner_id bigint unsigned,
	constraint fk명 foreign key (onwer_id) references owners (owner_id)
)
```

## #8.4 ON DELETE

`foreign key (onwer_id) references owners (owner_id) on delete`
- CASCADE
	- 관련된 레코드가 삭제되면 그것과 연결된 다른 레코드도 삭제 된다.
- NO ACTION
- RESTRICT
- SET NULL
	- table이 삭제되면 해당 왜래키를 null로 설정한다.
	- NOT NULL 제약 확인

## #8.5 One-To-Many and One-To-One
[https://dbdiagram.io/](https://dbdiagram.io/)

## #8.6 Many-To-Many

### bridge table or link table
- 없이 N:M은 표현자체가 불가능하다.

### composite key(복합키)
- primary key가 두 개이상의 컬럼으로 구성된 것을 의미한다.

```sql
CREATE TABLE dogs
(
    dog_id        BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name          VARCHAR(50) NOT NULL,
    weight        DECIMAL(5, 2),
    date_of_birth DATE,
    onwer_id      BIGINT UNSIGNED,
    breed_id      BIGINT UNSIGNED default 2,
    -- foreign key (onwer_id) references owners (owner_id) on delete set null,
    CONSTRAINT breed_fk foreign key (breed_id) references breeds (breed_id) on delete set default
);

alter table dogs
    drop foreign key owner_fk add constraint owner_fk foreign key (onwer_id) references owners (owner_id) on delete set null;

create table owners
(
    owner_id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name     VARCHAR(50) NOT NULL,
    email    VARCHAR(100) UNIQUE,
    phone    VARCHAR(20),
    address  TINYTEXT

);

create table breeds
(
    breed_id         BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name             VARCHAR(50) NOT NULL,
    size_category    ENUM ('small', 'medium', 'big') DEFAULT 'small',
    typical_lifespan TINYINT
);

create table pet_passports
(
    pet_passport_id   BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    blood_type        varchar(10),
    allergies         TEXT,
    last_checkup_date Date,
    dog_id            BIGINT UNSIGNED unique,
    foreign key (dog_id) references dogs (dog_id) on delete cascade
);

create table tricks
(
    trick_id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name     VARCHAR(50) NOT NULL UNIQUE,
    difficulty ENUM('easy', 'medium', 'hard') not null default 'easy'
);

create table dog_tricks
(
    dog_id BIGINT UNSIGNED,
    trick_id BIGINT UNSIGNED,
    proficiency enum('beginner', 'intermediate', 'expert') not null default 'beginner',
    date_learned timestamp default current_timestamp,
    primary key (dog_id, trick_id),
    foreign key (dog_id) references dogs (dog_id) on delete cascade,
    foreign key (trick_id) references tricks (trick_id) on delete cascade
);
```