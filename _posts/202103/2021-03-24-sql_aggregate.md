---
title:  "[RDBMS] SQL Aggregate Function"
excerpt: "SQL 집계함수 정리"

categories:
  - Database

last_modified_at: 2021-03-24T18:30:00
---

- 한 컬럼의 데이터를 계산, 하나의 값으로 반환
- `GROUP BY` 구문으로 하나 또는 다수의 컬럼에 의한 결과를 그룹핑
- `HAVING` 구문으로 WHERE과 같이 필터링 가능 (그룹함수 or SELECT 하는 컬럼만 필터링)


### Functions
- COUNT : 해당 컬럼의 row 수
- SUM : 해당 컬럼의 합
- MIN, MAX : 해당 컬럼의 최소, 최대
- AVG : 해당 컬럼의 평균
- 이 외에도 많음

### GROUP BY, HAVING
- 항상 aggregate function이랑 같이 사용
- 특정 컬럼들을 그룹핑하여, 그 기준으로 특정 컬럼들과 aggregate function 값을 조회
- `HAVING`은 WHERE과 같은 필터링 기능 (그룹함수 or SELECT 하는 컬럼만 필터링)

### sql example

```sql
-- COUNT
SELECT COUNT(*) FROM customers;

-- SUM
SELECT SUM(no_seats) FROM rooms;

-- MIN, MAX
SELECT MAX(length_min) FROM films;
SELECT MIN(length_min) FROM films;

-- AVG
SELECT AVG(length_min) FROM films

-- EX : Count the number of screenings for Blade Runner 2049
SELECT COUNT(*) FROM screenings
JOIN films ON films.id = screenings.film_id
WHERE films.name = 'Blade Runner 2049';

-- GROUP BY : 집계함수 외의 컬럼을 그룹핑 해주어야함
SELECT customer_id, screening_id, COUNT(id) FROM bookings
GROUP BY customer_id, screening_id
HAVING customer_id = 10;

-- EX : Select the film name and count the number of screenings
--      for each film that is over 2 hours long
SELECT f.name, f.length_min, COUNT(s.id) FROM screenings s
JOIN films f ON f.id = s.film_id
GROUP BY f.name, f.length_min
HAVING f.length_min > 120;
-- 이 구문에서 몇 번 틀렸음.
-- SELECT에서 length_min을 넣지 않고 HAVING에서 length_min > 120 을 사용하니 계속 틀렸음
-- HAVING은 SELECT 하는 컬럼만 필터링 가능
```


----
**ref :**  
[집계 함수(Transact-SQL)](https://docs.microsoft.com/ko-kr/sql/t-sql/functions/aggregate-functions-transact-sql?view=sql-server-ver15)  
