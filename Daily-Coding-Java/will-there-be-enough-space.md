Daily Codewars #2019-03-06
--------------------------

### Question

**문제링크** : [[8 kyu]Will there be enough space?](https://www.codewars.com/kata/will-there-be-enough-space)

The Story: Bob is working as a bus driver. However, he has become extremely popular amongst the city's residents. With so many passengers wanting to get aboard his bus, he sometimes has to face the problem of not enough space left on the bus! He wants you to write a simple program telling him if he will be able to fit all the passengers. Task Overview: You have to write a function that accepts three parameters:

cap is the amount of people the bus can hold excluding the driver. on is the number of people on the bus. wait is the number of people waiting to get on to the bus. If there is enough space, return 0, and if there isn't, return the number of passengers he can't take.

Usage Examples:

```
>>> enough(10, 5, 5)
0 # He can fit all 5 passengers
>>> enough(100, 60, 50)
10 # He can't fit only 10 out of 50 waiting
```

### My Solution

```java
public class Bob {
  public static int enough(int cap, int on, int wait){
	  int remainingNumber = cap - on;
	  return remainingNumber >= wait ? 0 : wait - remainingNumber;
  }
}
```

> 조건연산자로 해결하는 간단한 방법이 생각나서 썻는데 다른 사람 해결책 보니 더 좋은 방법인 많았다. 더 없을 것 같았는데....

### @shadowmanos Solution

```java
class Bob {
    static int enough(final int capacity, final int alreadyOn, final int waiting){
        return Math.max(0, waiting + alreadyOn - capacity);
    }
}

```

> Math.max 함수를 사용할 생각은 전혀 하지 못했다. 아주 예전에 사용했던 적이 있었던 것 같긴한데 이 메소드는 잊고 있었다. 최소가 자리수 계산한게 0보다 작을시 0이고 크면 큰 수를 나오게 하는 이상황에 적절한 함수인 것 같다.
>
> Math.Max()는 입력받은 두 인자 값 중 큰 값을 리턴하는 함수 입니다. min() 함수와 반대 개념의 함수 입니다.

### @russfre Solution

```java
public class Bob {
  public static int enough(int cap, int on, int wait){
    return Math.max(0, on + wait - cap);
  }
}
```

> @shadowmanos 과 동일한 방법이다.

### 결론

-	1
-	2
-	3
