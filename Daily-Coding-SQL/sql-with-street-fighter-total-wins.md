Daily Codewars #2019-03-02
--------------------------

### Question

**문제링크** : [[7 kyu]SQL with Street Fighter: Total Wins)](https://www.codewars.com/kata/sql-with-street-fighter-total-wins)

It's time to assess which of the world's greatest fighters are through to the 6 coveted places in the semi-finals of the Street Fighter World Fighting Championship. Every fight of the year has been recorded and each fighter's wins and losses need to be added up.

Each row of the table `fighters` records, alongside the fighter's name, whether they won (1) or lost (0), as well as the type of move that ended the bout.

-	id
-	name
-	won
-	lost
-	move_id

winning_moves

-	id
-	move

However, due to new health and safety regulations, all ki blasts have been outlawed as a potential fire hazard. Any bout that ended with `Hadoken, Shouoken` or `Kikoken` should not be counted in the total wins and losses.

So, your job:

Return `name, won`, and `lost` columns displaying the name, total number of wins and total number of losses. Group by the fighter's name. Do not count any wins or losses where the winning move was `Hadoken, Shouoken` or `Kikoken`. Order from most-wins to least Return the top 6. Don't worry about ties.

### My Solution

```sql
SELECT F.name AS name, SUM(F.won) AS won, SUM(F.lost) AS lost
FROM fighters F, winning_moves WM
WHERE F.move_id = WM.id
	AND WM.move NOT IN ('Hadoken', 'Shouoken', 'Kikoken')
GROUP BY F.name  
ORDER BY won DESC
LIMIT 6;
```

### @cpailler Solution

```sql
SELECT name, sum(won) as won, sum(lost) as lost FROM fighters
INNER JOIN winning_moves ON fighters.move_id=winning_moves.id
WHERE NOT move IN ('Hadoken', 'Shouoken', 'Kikoken')
GROUP BY name
ORDER by won DESC
LIMIT 6;
```

> 내가 코딩한 것과 비슷한데. 이번에 쿼리 짜면서 알게 된것이 GROUP BY, ORDER BY 할때 해당 테이블에 컬럼 값으로 하지말고 SELECT 되는 컬럼을 기준으로 해야겠다.

### 결론

-	영어 독해를 잘 못해서 문제를 이해를 잘 못해서 간단한 건데 푸는데 오래 걸렸다. 테이블이 두개인 것은 헤메다가 알게 되어 풀었다.  
-	그리고 나는 지금까지 ORDER BY, GROUP BY 할때 테이블에 컬럼 값을 기준으로 했었는데 이번에 보니 SELECT 문에 컬럼 기준으로 해야한다는 것을 이제야 알게 되었다...참 바보같네.
-	codewars SQL 문제 푸는 것은 에러 검출이 보기 어려워서 쿼리 짜는데 에러 나는데 애먹었다. ㅠㅠ
