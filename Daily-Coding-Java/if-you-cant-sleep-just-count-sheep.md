Daily Codewars #2019-03-01
--------------------------

### Question

**문제링크** : [[8 kyu]If you can't sleep, just count sheep!!](https://www.codewars.com/kata/if-you-cant-sleep-just-count-sheep)

If you can't sleep, just count sheep!!

Task: Given a non-negative integer, 3 for example, return a string with a murmur: `"1 sheep...2 sheep...3 sheep..."` . Input will always be valid, i.e. no negative integers.

### My Solution

-	Java 8 이전

```java
class Kata {
	public static String countingSheep(int num) {
		StringBuilder result = new StringBuilder();

		for (int i = 0; i < num; i++) {
			result.append(String.valueOf(i+1).concat(" sheep..."));
		}

		return result.toString();		
	}
}
```

-	Java 8

```java
import java.util.stream.Collectors;
import java.util.stream.IntStream;

class Kata {
	public static String countingSheep(int num) {		
		return IntStream.range(1, num+1)
        .mapToObj(i -> String.valueOf(i).concat(" sheep..."))
        .collect(Collectors.joining());				
	}
}
```

> 아주 쉬운 문제이다. 일반적인 방법은 성능을 고려해 StringBuilder를 사용해서 문자열을 추가했고 내부에서는 concat으로 더했다. 두글자를 더할시는 concat 그외에 많을시는 StringBuilder나 + 를 사용해서 더하는 것이 성능이 좋다는 것을 알고 해당 사항을 적용했다. 그리고 Java8은 IntStream을 사용했고 range를 사용해 int 배열을 생성 후 처리를 했다.

### @pimentel Solution

```java
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Kata {
  public static String countingSheep(int num) {
    return IntStream.rangeClosed(1, num)
                    .mapToObj(i -> i + " sheep...")
                    .collect(Collectors.joining());
  }
}

```

> 나와 비슷하다. 다른 점은 나는 **range** 를 사용하였는데. 이분은 **rangeClosed** 를 사용했다. 두개의 차이는 IntStream.range(1, 3);  
> // > 1, 2 IntStream.rangeClosed(1, 3);  
> // > 1, 2, 3 이다.

### @dbertee Solution

```java
class Kata {
    public static String countingSheep(int num) {
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 1; i <= num; i++) {
            stringBuilder.append(i).append(" sheep...");
        }
        return stringBuilder.toString();
    }
}
```

> 아.... concat쓸 필요없이 그냥 append 하면 됐었겠네... 생각을 못했다. ㅠㅠ

### @user5898652 Solution

```java
import java.util.stream.IntStream;

class Kata {
    private static final String APPENDIX = " sheep...";

    public static String countingSheep(int num) {
        return ints(num).collect(StringBuilder::new, Kata::accept, Kata::idle).toString();
    }

    private static IntStream ints(int last) {
        return IntStream.rangeClosed(1, last);
    }

    private static void accept(StringBuilder stringBuilder, int i) {
        stringBuilder.append(i).append(APPENDIX);
    }

    private static void idle(StringBuilder a, StringBuilder b) {      
        return;
    }        
}
```

> 소스는 양이 많아 보이지만 각각의 기능을 메소드로 정리했고 각 기능을 **ints(num).collect(StringBuilder::new, Kata::accept, Kata::idle).toString();** 게 처리한 것이 인상적이다.

### @dieterkindt Solution

```java
class Kata {
    public static String countingSheep(int num) {
        StringBuilder result = new StringBuilder();
        for (int i = 1; i <= num; i++) {
            result.append(String.format("%d sheep...", i));
        }
        return result.toString();
    }
}
```

> **String.format("%d sheep...", i)** 을 사용한게 인상적이다.

### 결론

-	이번에 여러 문자열을 더할시 StringBuilder를 사용해야한다는 것을 다시 한번 더 생각하게 되었다.
-	range, rangeClosed의 차이를 알게 되었다.
-	IntStream도 오랜만에 사용해 봤다.
