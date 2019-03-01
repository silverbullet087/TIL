Daily Codewars #2019-03-01
--------------------------

### Question

**문제링크** : [[8 kyu]Abbreviate a Two Word Name](https://www.codewars.com/kata/abbreviate-a-two-word-name)

Write a function to convert a name into initials. This kata strictly takes two words with one space in between them.

The output should be two capital letters with a dot seperating them.

It should look like this:

Sam Harris => S.H

Patrick Feeney => P.F

### My Solution

-	Java 8 이전

```java
import java.util.Arrays;
import java.util.stream.Collectors;

public class AbbreviateTwoWords {

  public static String abbrevName(String name) {
    return name.split(" ")[0].toUpperCase().charAt(0) + "." + name.split(" ")[1].toUpperCase().charAt(0);
  }
}
```

-	Java 8

```java
import java.util.Arrays;
import java.util.stream.Collectors;

public class AbbreviateTwoWords {

  public static String abbrevName(String name) {
	   return Arrays.stream(name.split(" "))
  			.map(String::toUpperCase)
  			.map(n -> n.substring(0, 1))
  			.collect(Collectors.joining("."));
  }
}
```

### @dinglemouse Solution

```java
public class AbbreviateTwoWords {

  public static String abbrevName(String name) {
    return name.toUpperCase().replaceAll("(.).*\\s(.).*", "$1.$2");
  }

}
```

> 와우! 정규표현식은 위대하다. 한줄로 코딩은 끝나는구나. 아직 정규표현식을 제대로 공부를 하지 못해서 코딩하기엔 무리지만 정규표현식이 정말 대단한 것 같다. 나중에 꼭 공부해야겠다.

### @Velimir10 Solution

```java
public class AbbreviateTwoWords {

 public static String abbrevName(String name) {

        String[] init = name.split(" ");
        return init[0].substring(0, 1).toUpperCase().concat("."+ init[1].substring(0, 1).toUpperCase());
    }
}
```

> 난 그냥 String + "." String 으로 문자를 붙였는데 concat을 쓸 것은 생각을 못했다. 아무래서 성능상 String 을 따로 써서 String 객체가 각각 생성 되게 하는 것보다. .concat으로 붙이는 것이 더 좋은 방법 같다.

### @scottyboutin Solution

```java
import java.util.Arrays;
import java.util.stream.Collectors;

public class AbbreviateTwoWords {

  public static String abbrevName(String name) {
    return Arrays.stream(name.split(" "))
                 .map(String::toUpperCase)
                 .map(word -> word.substring(0, 1))
                 .collect(Collectors.joining("."));

  }

}
```

> Java8도 한줄로 코딩이 가능하고 좋다.

### 결론

-	아주 쉬운 문제였지만 역시 다른 사람들의 해결책을 보니 더 좋고 다양한 방법이 있다는 것을 알게 되었다. 앞으로 난이도는 낮은 문제들을 풀어도 배울점이 많을 것 같다.
-	정규표현식을 통해 코딩 하는 것이 상당히 좋아 보인다. 반드시 정규표현식은 시간을 할애해서 공부를 해야겠다.
-	Java8로 코딩하는 습관을 들여야겠다.
