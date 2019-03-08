Daily Codewars #2019-03-08
--------------------------

### Question

**문제링크** : [[8 kyu]Grasshopper - Summation](https://www.codewars.com/kata/grasshopper-summation)

Summation Write a program that finds the summation of every number from 1 to num. The number will always be a positive integer greater than 0.

For example:

```
summation(2) -> 3
1 + 2

summation(8) -> 36
1 + 2 + 3 + 4 + 5 + 6 + 7 + 8

```

### My Solution

-	Java 8 이전

```java
public class GrassHopper {

    public static int summation(int n) {
      int result = 0;

      for (int i = 0; i < n; i++) {
        result += i + 1;
      }

      return result;    	
    }
}
```

-	Java 8

```java
import java.util.stream.IntStream;

public class GrassHopper {

    public static int summation(int n) {    	
    	return IntStream.range(1, n + 1).sum();    	
    }
}
```

> 쉬운 문제였다.

### @Beast Solution

```java
public class GrassHopper {

    public static int summation(int n) {

        return  n*(n+1)/2;
    }
}

```

> 1+2+3+4+5+6+7+9+10을 어떻게 빠르게 계산합니까? 라는 문제는 수학에서 기초적인 문제인데 너무 오랜만에 봤더니 수학적으로 쉽게 푸는 방법을 잊고 있었다. 위 코드 해답은 그 쉬게 푸는 공식이 적용된 코드이다. 생각을 못했다.
>
> (1+10=11)... (2+9=11)... 가 n/2개여서 위 공식을 적용할 수 있다.

### @Cs4r Solution

```java
import java.util.stream.IntStream;

public class GrassHopper {

    public static int summation(int n) {

        return IntStream.rangeClosed(1,n).sum();
    }
}
```

> 이전 다른 문제에서도 나는 range를 사용했는데 이번에도 range를 사용했다. range와 rangeClosed 차이는 알고 있는데... n+1로 할바엔 rangeClosed 쓰는게 좋았을텐데 아쉽다.

### @fkubala Solution

```java
public class GrassHopper {

    public static int summation(int n) {
        if (n == 1)
          return 1;
        return summation(n-1) + n;
    }
}
```

> 이야~ 생각도 못했는데 독특한 소스다. 재귀호출을 사용했다.

### 결론

-	range와 rangeClosed 차이를 알고 상황에 맞춰 적절하게 사용하자.
-	수학 공부도 좀 해야겠다...
-	재귀호출을 오랜만에 봤네...
