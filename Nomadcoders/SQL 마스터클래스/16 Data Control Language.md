## #16.0 Introduction

### DCL
- 사용자가 데이터베이스를 조회하고 수정할 수 있는 권한을 설정할 수 있게 해준다.
## #16.1 Users
```sql
create role marketer with login password 'marketing4ever';  
  
grant select on users to marketer;  
  
grant select, insert on statuses, directors to marketer;  
  
grant select on all tables in schema public to marketer;  
  
revoke insert on statuses, directors from marketer;  
  
grant insert on all tables in schema public to marketer;  
  
revoke insert on all tables in schema public from marketer;
```
- grant
- revoke

## #16.2 Roles

