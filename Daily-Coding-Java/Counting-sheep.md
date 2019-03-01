Daily Codewars #2
-----------------

### Question

[Counting sheep...](https://www.codewars.com/kata/counting-sheep-dot-dot-dot/java) - https://www.codewars.com/kata/counting-sheep-dot-dot-dot/java

-	몇몇 양들이 그들의 장소에서 사라질 수있는 양들의 배열을 생각해보십시오. 배열에있는 양의 개수를 계산하는 함수가 필요합니다 (true는 나타남을 의미 함).

### My Solution

```java
public class Counter {
    public int countSheeps(Boolean[] arrayOfSheeps) {

        int result = 0;

        List<Boolean> SheepsList = new ArrayList<Boolean>();
        Collections.addAll(SheepsList, arrayOfSheeps);

        for (Boolean Sheeps : SheepsList) {
            if (Sheeps == null) continue;
            if (Sheeps.booleanValue() == true) result++;
        }

        return result;
    }
}

public class CounterTest {
    Boolean[] array1 = {true,  true,  true,  false,
            true,  true,  true,  true ,
            true,  false, true,  false,
            true,  false, false, true ,
            true,  true,  true,  true ,
            false, false, true,  true };

    @Test
    public void test() {
        assertEquals("There are 17 sheeps in total", 17, new Counter().countSheeps(array1));
    }
}
```

> 8kyu 라서 그런지 난이도가 높지 않고 쉬웠다.

### @mortonfox Solution

```java
public class Counter {
  public int countSheeps(Boolean[] arrayOfSheeps) {
    int count = 0;
    for (Boolean b : arrayOfSheeps) if (b) count++;
    return count;
  }
}
```

> @mortonfox 코딩 한 것을 보니 난 참 바보같이 코딩 한 것 같다. 배열을 다루는게 싫어서 ArrayList로 변환해서 했는데 어짜피 향상된 for문 돌릴 것 굳이 ArrayList로 변환 할 필요가 없었다.

### @Abbe Solution

```java
import java.util.Arrays;

public class Counter {
  public int countSheeps(Boolean[] arrayOfSheeps) {
    return (int) Arrays.stream(arrayOfSheeps).filter(Boolean::booleanValue).count();
  }
}
```

> 처음엔 이게 뭔가 싶었는데 검색해 보니 Java8을 이용한 소스였다. 말로만 듣던 자바8을 사용하여 한줄로 끝냈다. 놀랍고 당황스럽다. Java8 책을 사 놓고 아직 안 보고 있는데 빨리 보고 싶다. 나도 Java8로 코딩해보고 싶다.
