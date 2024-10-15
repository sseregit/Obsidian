## #9.0 Introduction

## #9.1 CROSS JOIN

### cross join
- table row * join table row 수가 select 된다.

FROM -> JOIN -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY

## #9.2 INNER JOIN

### inner join
- 어떤 row와 row를 연결시킬지 선택할 수 있다.
```sql
select ...
  from dogs  
join owners using (owner_id)  
join breeds using (breed_id)  
;
```
- using 키워드로 on 절을 줄일 수 있다.

## #9.3 OUTER JOIN