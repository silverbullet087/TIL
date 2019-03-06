Daily Codewars #2019-03-06
--------------------------

### Question

**문제링크** : [[8 kyu]A Strange Trip to the Market](https://www.codewars.com/kata/a-strange-trip-to-the-market)

You're on your way to the market when you hear beautiful music coming from a nearby street performer. The notes come together like you wouln't believe as the musician puts together patterns of tunes. As you wonder what kind of algorithm you could use to shift octaves by 8 pitches or something silly like that, it dawns on you that you have been watching the musician for some 10 odd minutes. You ask, "How much do people normally tip for something like this?" The artist looks up. "Its always gonna be about tree fiddy."

It was then that you realize the musician was a 400 foot tall beast from the paleolithic era. The Loch Ness Monster almost tricked you!

There are only 2 guaranteed ways to tell if you are speaking to The Loch Ness Monster: A.) It is a 400 foot tall beast from the paleolithic era B.) It will ask you for tree fiddy

Since Nessie is a master of disguise, the only way accurately tell is to look for the phrase "tree fiddy". Since you are tired of being grifted by this monster, the time has come to code a solution for finding The Loch Ness Monster. Note: It can also be written as 3.50 or three fifty.

### My Solution

-	Java 8 이전

```java
public class Nessie {
    public static boolean isLockNessMonster(String s){
    	return s.contains("tree fiddy") || s.contains("three fifty") || s.contains("3.50");
    }
}
```

-	Java 8

```java
import java.util.Arrays;

public class Nessie {
    public static boolean isLockNessMonster(String s){
    	String[] strs = {"tree fiddy", "three fifty", "3.50"};
    	return Arrays.stream(strs).anyMatch(str -> s.contains(str));
    }
}
```

> 쉬운 문제인데 문제 이해가 어려웠다. ㅡㅡ;;

### @nightroad35 Solution

```java
public class Nessie {
    public static boolean isLockNessMonster(String s){
      return s.contains("tree fiddy") || s.contains("3.50");
    }
}

```

> 나와 동일한 해결 방법이다.

### @Abbe Solution

```java
import java.util.regex.Pattern;

public class Nessie {
    public static boolean isLockNessMonster(String s) {
        return Pattern.matches(".*(tree fiddy|3\\.50|three fifty).*", s);
    }
}
```

> 문자열 내에서 문자를 찾을시 contains 외에 Pattern.matches 를 사용해서 찾을 수 있다는 것을 알고 있어야 겠다. 이 방법은 생각 못했다.

### @falsetru Solution

```java
public class Nessie {
    public static boolean isLockNessMonster(String s) {
        return s.indexOf("3.50") >= 0 || s.indexOf("tree fiddy") >= 0;
    }
}
```

> 이분은 indexOf를 사용해서 확인했다.

### 결론

-	문자열내에서 문자 찾는 방법은
-	1. contains 사용
-	2. Pattern.matches 사용
-	3. indexOf 사용
-	이 있다는 것을 확인하였다.
