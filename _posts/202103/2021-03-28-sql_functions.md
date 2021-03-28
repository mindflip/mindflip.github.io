---
title:  "[RDBMS] SQL Functions - String, Date"
excerpt: "자주 사용되는 문자열과 날짜 관련 함수 정리"

categories:
  - Database

last_modified_at: 2021-03-28T19:00:00
---

- Functions : SQL 내부에 저장되어 매개변수를 입력으로 받았을 때 특정 값을 반환


### String functions
- CONCAT : 두 문자열 이어주기
- SUBSTRING : 문자열 자르기
- UPPER, LOWER : 문자열 대소문자 변환

```sql
-- concat인자로 여러 columns, values 들이 올 수 있음
SELECT CONCAT(first_name, " ", last_name) AS full_name FROM customers;

-- substring 첫 번째 인자는 타겟 문자열, 두 번째는 시작 문자 인덱스, 세 번째는 몇 번째까지 자를지 결정하는 값
SELECT SUBSTRING("Example", 3, 3) AS Sub;
SELECT SUBSTRING("Example", 3) AS Sub; -- 세 번째 이전 문자는 잘라내고, 나머지 문자열만 반환
SELECT SUBSTRING(name, -3) FROM films; -- 음수 값은 문자열의 끝쪽에서부터 반대로 진행(끝에서 세 번째 문자열부터 자르기)

-- 대소문자 변환
SELECT UPPER(last_name) FROM customers;
SELECT LOWER(last_name) FROM customers;
```


### Date functions
- DATE : 년도, 달, 날짜까지 다시 리턴
- MONTH : 달만 리턴
- YEAR : 년도만 리턴

```sql
SELECT DATE('2021-03-21');
-- return '2021-03-21'
SELECT * FROM screenings
WHERE DATE(start_time) BETWEEN '2017-10-03' AND '2017-10-05';
-- 그냥 start_time 하면 2017-10-05 00:00:00 로 인식해서 4일까지 데이터만 조회

SELECT MONTH('2018-06-05 05:44:23');
-- return '6'

SELECT YEAR('2018-06-05 05:44:23');
-- return '2018'
```

----
**ref :**  
[String Functions (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/string-functions-transact-sql?view=sql-server-ver15)  
[Date and Time Data Types and Functions (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql?view=sql-server-ver15)  
