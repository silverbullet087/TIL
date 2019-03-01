Daily Codewars #2019-03-01
--------------------------

### Question

**문제링크** : [[8 kyu]Keep Hydrated!](https://www.codewars.com/kata/keep-hydrated-1/sql)

Nathan loves cycling.

Because Nathan knows it is important to stay hydrated, he drinks 0.5 litres of water per hour of cycling.

You get given the time in hours and you need to return the number of litres Nathan will drink, rounded to the smallest value.

For example:

time = 3 ----> litres = 1

time = 6.7---> litres = 3

time = 11.8--> litres = 5

You have to return 3 columns: **id**, **hours** and **liters** (not litres, it's a difference from the kata description)

### My Solution

```SQL
SELECT id, hours, trunc(hours* 0.5)  AS liters FROM cycling
```

> 구글링해서 trunc이 소수점 버림이라는 것을 알고 해결했다.

### @Beast Solution

```SQL
SELECT *, floor(hours / 2) as liters FROM cycling
```

> 정수값만 나오게 해서 소수점을 제거 했다.

### @pmclarnon Solution

```SQL
ALTER TABLE cycling
ADD COLUMN liters INTEGER;

UPDATE cycling
SET liters=FLOOR(hours*0.5);

SELECT * FROM cycling;
```

> codewars SQL 문제는 테이블 수정해서 할 수가 있구나...

### 결론

-	ROUND(숫자,반올림할 자릿수) - 숫자를 반올림할 자릿수 +1 자릿수에서 반올림
-	TRUNC(숫자,버릴 자릿수) - 숫자를 버릴 자릿수 아래로 버림
-	FLOOR : 지정한 값보다 작은 수 중에서 가장 큰 정수
-	쉬운 SQL 문제였다. 소수점 버림만 할 줄 알면 풀 수 있는...
-	쿼리 짜는 능력을 향상 시킬 수 있는 문제를 풀고 싶다.
-	지금 알게 된 것인데 SQL만 해당하는 문제인 문제가 따로 있는 것 같다. 쿼리짜는 능력을 향상 시킬 수 있는 문제로 풀어야겠다.
