Daily Codewars #2019-02-24
--------------------------

### Question

**문제링크** : [[8 kyu]Total amount of points Theater](https://www.codewars.com/kata/total-amount-of-points)

Our football team finished the championship. The result of each match look like "x:y". Results of all matches are recorded in the collection.

For example: ["3:1", "2:2", "0:1", ...]

Write a function that takes such collection and counts the points of our team in the championship. Rules for counting points for each match:

if x>y - 3 points if x<y - 0 point if x=y - 1 point Notes:

there are 10 matches in the championship 0 <= x <= 4 0 <= y <= 4

### My Solution

```java
public class TotalPoints {

    public static int points(String[] games) {
    	int totalPoint = 0;

    	for (String game : games) {
    		String[] point = game.split(":");
    		int x = Integer.parseInt(point[0]);
    		int y = Integer.parseInt(point[1]);

    		if (x > y) {
    			totalPoint += 3;
			}
    		if (x < y) {
    			totalPoint += 0;
    		}
    		if (x == y) {
    			totalPoint += 1;
    		}
		}

    	return totalPoint;

    }
}
```

> 해결책으로 코딩한 것은 무난하나 더 요약해서 간단하게 코딩이 가능한데 생각을 못했다.

### @a.2.c.4 Solution

```java
public class TotalPoints {

    public static int points(String[] games) {
        int sum = 0;

        for (String s : games) {
          char x = s.charAt(0),
               y = s.charAt(2);

          sum += x > y ? 3 : x == y ? 1 : 0;
        }

        return sum;
    }
}
```

> 나는 split로 나눴는데. 이분은 굳이 split로 나눌필요없이 charAt로 x,y값을 추출 했다. 그리고 삼항연산자(조건연산자)를 사용하여 승,무,패 점수를 계산하였다. 나 보다 훨씬 소스가 간결한다.

### @clvcj16 Solution

```java
public class TotalPoints {

    public static int points(String[] games) {
      int total = 0;
        for(String s : games){
          int x = Integer.parseInt(s.split(":",2)[0],10);
          int y = Integer.parseInt(s.split(":",2)[1],10);
          if(x > y){ total += 3;}
          if(x == y){ total += 1;}
        }
      return total;
    }
}
```

> 나와 비슷한데 더 요약되어 코딩되어 있다. 졌을때는 0을 더하므로 굳이 해당사항을 더할 필요 없다는 것을 알게 되었다. 그리고 split뒤에 [index]로 바로 값을 가지고 올것은 생각 못했다.

### @dkrasilov Solution

```java
public class TotalPoints {

    public static int points(String[] games) {
      return Stream.of(games)
        .map(s -> s.split(":"))
        .map(arr -> {
          int x = Integer.parseInt(arr[0]);
          int y = Integer.parseInt(arr[1]);
          if (x > y) return 3;
          if (x < y) return 0;
          return 1;
        })
        .mapToInt(value -> value)
        .sum();     
      //implement me
    }
}
```

> 이분은 java8을 활용해서 코딩했다. 나도 java8로 stream으로 for문 돌리는 것 밖에 생각 못했고 하다가 포기하고 일반적인 방법으로 했는데 map을 활용할 생각을 하지 못했다.

### 결론

-	자바8에 Stream, map, mapToInt, sum을 사용해서 충분히 자바8을 사용해서 개발 가능한 것이였다.
-	조건연산자를 사용해서 if문을 한줄로 코딩이 가능했다.
-	정해진 문자열이어서 charAt를 사용하기도 충분했다.
