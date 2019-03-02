Daily Codewars #2019-03-02
--------------------------

### Question

**문제링크** : [[8 kyu]Adults only (SQL for Beginners #1)](https://www.codewars.com/kata/adults-only-sql-for-beginners-number-1)

In your application, there is a section for adults only. You need to get a list of names and ages of users from the users table, who are 18 years old or older.

users table schema

name age NOTE: Your solution should use pure SQL. Ruby is used within the test cases to do the actual testing.

This kata is part of a collection of SQL challenges for beginners. You can take the rest of the challenges here!

### My Solution

```sql
SELECT name, age
FROM users
WHERE age >= 18
```

### @jalaniz1 Solution

```sql
SELECT name, age FROM users WHERE age >= 18;
```

> 여러 코드들이 나와 이유저와 비슷하게 쿼리를 짰다.

### 결론

-	난이도가 너무 쉽다.
-	8 kyu 난이도는 너무 낮은 것 같다. 윗 단계를 해봐야겠다.
