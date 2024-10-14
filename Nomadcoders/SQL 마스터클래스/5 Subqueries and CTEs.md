## #5.0 Introduction

## #5.1 Independent Subqueries

### independent subquery
- 어떤 행을 실행하고 있는지에 따라 도출되는 결과값이 달라지지 않는다.

데이터 베이스들은 **쿼리 플래너**가 존재하고 쿼리 플래너는 쿼리를 최대한 최적화 시켜준다.

## #5.2 CTEs

### uncorrelated subquery

### CTE
- Common Table Expression
- independent subquery를 재사용할 수 있게 해준다.

## #5.3 Correlated Subqueries

### correlated subquery
- 메인 쿼리가 어떤 열에서 실행중인지에 따라 결과값이 달라진다.

where 조건의 순서는 query optimizer가 더 실행 비용이 저렴한 subquery를 먼저 실행시켜준다.

## #5.4 Correlated CTEs

## #5.5 Subquery Practice

## #5.6 Final Practice