Daily Codewars #1
-----------------

### Question

[Money, Money, Money](https://www.codewars.com/kata/money-money-money/java) - https://www.codewars.com/kata/money-money-money/java

-	투자하고자하는 금액 'P'를 가지고 있으며이 금액이 'D'에 이르기 위해이 금액을 은행에 몇 년 동안 보관해야 하는지를 구하는 문제다.

### My Solution

```java
public class Money {
    public static int calculateYears(double principal, double interest,  double tax, double desired) {
        // your code

        double InterestCal = 0;
        double taxCal = 0;
        double principalAfter1stYear = 0;
        double annualAmount = principal;

        int year = 0;

        while (annualAmount != desired && desired > principalAfter1stYear) {
            InterestCal = annualAmount * interest;
            taxCal = InterestCal * tax;
            principalAfter1stYear = annualAmount + InterestCal - taxCal;
            annualAmount = principalAfter1stYear;

            year++;
        }

        return year;
    }
}
```

> 처음으로 Codewars에서 문제를 풀어 봤다. 금액 계산 공식을 몰라서 시간을 많이 소비 했다. 금액 계산 공신만 알면 쉬운 문제였다. 단, 단순히 돌아가게 코딩을 했더니 소스가 지저분하다. 개선해야할 부분이 많이 보인다.

@Darnor Solution

```java
public class Money {
  public static int calculateYears(double principal, double interest, double tax, double desired) {
    int years = 0;
    while (principal < desired) {
      principal += principal * interest * (1 - tax);
      years++;
    }
    return years;
  }
}
```

> 아... 리팩토링 책에서 매개변수에 데이터 저장하는게 좋지 않다는 것을 봐서 principal 매개변수에 데이터를 저장하지 않고 annualAmount 변수를 사용했는데 그렇다 보니 소스가 더욱 더 지저분해졌다. principalAfter1stYear 변수를 굳이 사용할 필요가 없었는데 잘 못 사용을 해서 while문 조건문이 더 길어지고 while 내부 코드도 길어졌다. 그리고 계산 공식도 위 코드와 같이 개선할 수 있었는데 아쉽다.

@huynhrichy Solution

```java
public class Money {
  public static int calculateYears(double principal, double interest,  double tax, double desired) {
    int years = 0;

    while (principal < desired) {
      years++;
      principal += (principal * interest) - (principal * interest * tax);
    }

    return years;
  }
}
```

> 최소한 공식은 위 코드처럼 한줄로 정리해서 코딩했으면 하는 아쉬움이 남는다. 그럼 @Darnor와 같은 계산 방식도 생각 가능했을텐데...
