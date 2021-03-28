---
title:  "[RDBMS] SQL Subquery"
excerpt: "서브쿼리 - 쿼리 안의 쿼리"

categories:
  - Database

last_modified_at: 2021-03-28T18:30:00
---

- 다른 쿼리의 내부에서 실행되는 쿼리문
- SELECT, INSERT, UPDATE, DELETE 쿼리 내에 사용될 수 있음
- WHERE, FROM 구문에 사용될 수 있음
- 두 가지 종류의 subquery : `Non-correlated`, `Correlated`


### Non-correlated subquery
- 내부 쿼리가 다른 쿼리에 독립적으로 실행 가능
- 내부 쿼리가 처음으로 실행 후, 결과를 만들어 내고 외부 쿼리가 실행
- WHERE 또는 FROM 구문에 사용
- FROM에 사용시, derived table에는 alias를 반드시 사용

```sql
-- WHERE 구문의 Subquery
SELECT id, start_time FROM screenings
WHERE film_id in
(SELECT id FROM films
WHERE length_min > 120);

-- FROM 구문의 Subquery
-- 이때 내부 쿼리는 반드시 alias가 있어야함. 여기서는 'b'로 지정
SELECT AVG(no_seats), MAX(no_seats) FROM
(SELECT booking_id, COUNT(seat_id) AS no_seats FROM reserved_seat
GROUP BY booking_id) b; -- 내부 쿼리로 만들어진 테이블은 'derived table'이라고도 함
```


### Correlated subquery
- 내부 쿼리는 독립적으로 실행 불가능
- 내부 쿼리는 외부 쿼리에 의해 모든 row를 호출하기 위해 사용됨
- 실제 데이터를 낼 때는 내부 쿼리에 의해 도출되는 column은 alias 해주기

```sql
-- bookings에 해당하는 예약된 seat개수와 해당 예약의 관객, 상영 id 조회
SELECT screening_id, customer_id,
(SELECT COUNT(seat_id)
FROM reserved_seat WHERE booking_id = b.id)
FROM bookings b
ORDER BY screening_id;
```


----
**ref :**  
[Subqueries](https://docs.microsoft.com/en-us/sql/relational-databases/performance/subqueries?view=sql-server-ver15)  
