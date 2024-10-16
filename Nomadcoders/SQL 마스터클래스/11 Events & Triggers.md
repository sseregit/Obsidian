## #11.0 Introduction

### event
- MySQL에서 기본적으로 제공하는 기능
- PostgreSQL에서도 지원하지만 확장프로그램을 이용해야 한다.
- database가 해야 할 작업들을 스케줄링 할 수 있다.

### trigger
- database에서 일어나는 일에 우리가 반응할 수 있다.

## #11.1 Events

### delimiter
- database에게 SQL statement가 끝났다고 알려주는 문자 `;`

```sql
delimiter $$ -- event 생성 SQL의 바깥 부분에서만 적용된다.
create event archived_old_movies
    on schedule every 2 minute
        starts current_timestamp + interval 2 minute
    do
    begin
        insert into archived_movies
        select *
        from movies
        where release_date < year(curdate()) - 20;

        delete from movies where release_date < year(curdate()) - 20;
    end$$
delimiter ; -- event 생성 SQL의 바깥 부분에서만 적용된다.
```
- 특이한점은 begin end 안에 있는 statement를 `delimiter`를 변경해주지 않으면 여러개를 이해하지 못해서 `delimiter`를 변경하고 마지막에 다시 복구하는 식의 스크립트를 만들어야 한다.
## #11.2 Recap