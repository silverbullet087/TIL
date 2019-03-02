Daily Codewars #2019-03-02
--------------------------

### Question

**문제링크** : [[8 kyu]Sum of positive](https://www.codewars.com/kata/sum-of-positive)

You get an array of numbers, return the sum of all of the positives ones.

Example `[1,-4,7,12]` => `1 + 7 + 12 = 20`

Note: if there is nothing to sum, the sum is default to `0`.

### My Solution

-	Java 8 이전

```java
public class Positive{

  public static int sum(int[] arr){

	  int sum = 0;
	  for (int i : arr) {
		  if (i > 0) {
			  sum += i;
		  }
	  }
	  return sum;
	}

}
```

-	Java 8

```java
import java.util.Arrays;

public class Positive{

  public static int sum(int[] arr){
	  return Arrays.stream(arr).filter(n -> n > 0).sum();
	}

}
```

### @Boken Solution

```java
import java.util.Arrays;
public class Positive{
    public static int sum(int[] arr){
        return Arrays.stream(arr).filter(v -> v > 0).sum();
    }
}

```

> 나와 동일한 코드다. Java8은 좋다.

### @HarrySlaughter Solution

```java
public class Positive{
    public static int sum(int[] arr){
        int result = 0;
        for (int i : arr) {
            if (i > 0) {
                result += i;
            }
        }
        return result;
    }
}
```

> 이것도 나와 동일한 코드다. 심플히다.

### @Unnamed Solution

```java
import java.util.stream.IntStream;

public class Positive{

  public static int sum(int[] arr) {
    return IntStream.of(arr).filter(x -> x > 0).sum();
  }

}
```

> int[] 이여서 IntStream을 사용하였다. 성능상은 이게 더 좋은지도? IntStream을 사용할 것은 생각을 못했었다.

### 결론

-	int[] 을 stream을 사용할 때 Arrays.stream(arr)말고 IntStream을 사용해도 된다.
