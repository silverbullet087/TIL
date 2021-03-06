Daily Codewars #2019-02-24
--------------------------

### Question

**문제링크** : [[8 kyu]Simple Fun #1: Seats in Theater](https://www.codewars.com/kata/simple-fun-number-1-seats-in-theater)

**Task**

Your friend advised you to see a new performance in the most popular theater in the city. He knows a lot about art and his advice is usually good, but not this time: the performance turned out to be awfully dull. It's so bad you want to sneak out, which is quite simple, especially since the exit is located right behind your row to the left. All you need to do is climb over your seat and make your way to the exit.

The main problem is your shyness: you're afraid that you'll end up blocking the view (even if only for a couple of seconds) of all the people who sit behind you and in your column or the columns to your left. To gain some courage, you decide to calculate the number of such people and see if you can possibly make it to the exit without disturbing too many people.

Given the total number of rows and columns in the theater (nRows and nCols, respectively), and the row and column you're sitting in, return the number of people who sit strictly behind you and in your column or to the left, assuming all seats are occupied.

**Example**

For nCols = 16, nRows = 11, col = 5 and row = 3, the output should be

```
Theater.seats nCols nRows col row == 96
```

Here is what the theater looks like: ![](https://files.gitter.im/myjinxin2015/eAjZ/blob)

**Input/Output**

[input] integer nCols

An integer, the number of theater's columns.

Constraints: 1 ≤ nCols ≤ 1000.

[input] integer nRows

An integer, the number of theater's rows.

Constraints: 1 ≤ nRows ≤ 1000.

[input] integer col

An integer, the column number of your own seat (with the rightmost column having index 1).

Constraints: 1 ≤ col ≤ nCols.

[input] integer row

An integer, the row number of your own seat (with the front row having index 1).

Constraints: 1 ≤ row ≤ nRows.

[output] an integer

The number of people who sit strictly behind you and in your column or to the left.

### My Solution

```java
public class Kata {

  public static int seatsInTheater(int nCols, int nRows, int col, int row) {

    if(nCols < 1 || nCols > 1000){
      return 0;
    }

    if(nRows < 1 || nRows > 1000){
      return 0;
    }

    if(col < 1 || col > nCols){
      return 0;
    }

    if(row < 1 || row > nRows){
      return 0;
    }

    return (nRows - row) * (nCols - col + 1);

  }

}
```

> 다른 해결책과 비교해 봤을때 괜찮은 해결책이라고 생각한다.

### @Krzysiek014 Solution

```java
public class Kata {

  public static int seatsInTheater(int nCols, int nRows, int col, int row) {

    return (nCols-col+1)*(nRows-row);

  }

}
```

> 내가 코딩한 것과 비슷한데 이 해결책은 입력값 체크 로직이 누락되어 있다.

### @wilkotom Solution

```java
public class Kata {

  public static int seatsInTheater(int nCols, int nRows, int col, int row) {

    return (nRows - row) * (nCols - col + 1);

  }
}
```

> 이것도 마찬가지로 나와 비슷하고 입력값 체크 로직이 누락되어 있다.

### 결론

-	너무 쉬운 문제였는데. 베스트 해결책인 @Krzysiek014, @wilkotom 는 입력값 체크 로직이 빠져 있어 맞지 않는 소스라고 생각한다. 다른 몇몇 소스에서 입력값 체크 로직이 있으나 if문안에 if문이 있는 가독성이 떨어지는 소스들이었다.
