람다 표현식
-----------

### 람다란 무엇인가?

-	`람다 표현식`은 메서드로 전달할 수 있는 익명함수를 단순화한 것이다.

![람다 표현식-설명](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzTS1kVXE2UVBPWm8)

### 어디에, 어떻게 람다를 사용할까?

#### 함수형 인터페이스

-	`함수형 인터페이스`는 정확히 하나의 추상 메서드를 지정하는 인터페이스이다.
-	`전체 표현식을 함수형 인터페이스의 인스턴스로 취급`(기술적으로 따지면 함수형 인터페이스를 concrete 구현한 클래스의 인스턴스)할 수 있다.
-	`@Functionallnterface`는 함수형 인터페이스임을 가리키는 어노테이션이다.

#### 함수 디스크립터

-	함수형 인터페이스의 추상 메서드 시그너처는 람다 표현식의 시그너처를 가리킨다. 람다 표현식의 시그너처를 서술하는 메서드를 `함수 디스크립터`라고 부른다.

### 람다 활용: 실행 어라운드 패턴

-	실제 자원을 처리하는 코드를 설정과 정리 두 과정이 둘러싸는 형태를 `실행 어라운드 패턴`이라고 부른다.

![람다 활용: 실행 어라운드 패턴](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzVUJoV0hIdV9MLWM)

```java
public static String processFileLimited() throws IOException {
    try (BufferedReader br =
                 new BufferedReader(new FileReader("lambdasinaction/chap3/data.txt"))) {
        return br.readLine();
    }
}
```

#### 1단계: 동작 파라미터화를 기억하라

-processFile 메서드만 다른 동작을 수행하도록 할 때 processFile의 동작을 파라미터화하는 것이다.

```java
String twoLines = processFile((BufferedReader b) -> b.readLine() + b.readLine());
```

#### 2단계: 함수형 인터페이스를 이용해서 동작 전달

```java
@Functionallnterface
public interface BufferedReaderProcessor{
    public String process(BufferedReader b) throws IOException;
}

public static String processFile(BufferedReaderProcessor p) throws IOException {
	...
}
```

#### 3단계: 동작 실행!

```java
public static String processFile(BufferedReaderProcessor p) throws IOException {
    try(BufferedReader br = new BufferedReader(new FileReader("lambdasinaction/chap3/data.txt"))){
        return p.process(br);
    }
}
```

#### 4단계:람다 전달

```java
String oneLine = processFile((BufferedReader b) -> b.readLine());

String twoLines = processFile((BufferedReader b) -> b.readLine() + b.readLine());
```

### 함수형 인터페이스 사용

-	자바 8 라이브러리 설계자들은 java.util.function 패키지로 여러 가지 새로운 함수형 인터페이스를 제공한다.

#### Predicate

```java
@Functionallnterface
public interface Predicate<T> {
  boolean test(T t);
}

public static <T> List<T> filter(List<T> list, Predicate<T> p) {
  List<T> results = new ArrayList<>();
  for(T s: list) {
    if(p.test(s)) {
      results .add(s);
    }
  }
  return results;
}
Predicate<String> nonEmptyStringPredicate = (String s) -> !s.isEmpty();
List<String> nonEmpty = filter(listOfStrings, nonEmptyStringPredicate);
```

#### Consumer

```java
@Functionallnterface
public interface Consumer<T> {
  void accept(T t);
}

public static <T> void forEach(List<T> list, Consumer<T> c) {
  for(T i: list) {
    c.accept(i);
  }
}

forEach( Arrays.asList(1, 2, 3, 4, 5), (Integer i) -> System.out.println(i) );
```

#### Function

```java
@Functionallnterface
public interface Function<T, R> {
  R apply(T t);
}

public static <T, R> List<R> map(List<T> list,
Function<T, R> f) {
  List<R> result = new ArrayList<>();
  for (T s : list) {
    result.add(f.apply(s));
  }
  return result;
}

List<Integer> l = map(
                          Arrays.asList("lambdas", "in", "action"), (String s) -> s.length()
                      );
```

#### 기본형 특화

-	자바에서는 기본형을 참조형으로 변환할 수 있는 기능을 제공한다. 이 기능을 `박싱`이라고 한다. 반대로 참조형을 기본형으로 변환하는 것을 `언박싱`이라고 한다.
-	하지만 이런 변환 과정은 비용이 소모가 되고 자바 8에서는 특별한 버전의 함수형 인터페이스를 제공한다.

![기본형 특화](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzdlBhbFhEeVhMLWM)

#### 함수형 인터페이스와 람다 요약

![함수형 인터페이스와 람다 요약-1](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzcEgwdDFFRVJJZWc)

![함수형 인터페이스와 람다 요약-2](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzUTZ4cXJRUmZiVmM)

### 형식 검사, 형식 추론, 제약

#### 형식 검사

![형식 검사](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzUDBLUmFIWGY1QjQ)

#### 같은 람다, 다른 함수형 인터페이스

-	하나의 람다 표현식을 다향한 함수형 인터페이스에 사용할 수 있다.

```java
Comparator<Apple> c1 =
(Apple a1, Apple a2) -> a1.getWeight().compareTo(a2. getWeight());
TolntBiFunction<Apple, Apple> c2 =
(Apple a1, Apple a2) -> a1.getWeight().compareTo (a2.getWeight());
BiFunction <Apple, Apple, Integer> c3 =
(Apple a1, Apple a2) -> a1.getWeight ().compareTo(a2.getWeight());
```

-	List의 add 메서드는 Consumer 콘텍스트(T -> void)가 기대하는 void 대신 boolean을 반환하지만 유효한 코드다.

```java
// Predicate는 불 린 반환값을 강는다.
Predicate<String> p = 5 -> list.add(s);
// Consumer는 void 반환값을 갚는다.
Consumer<String> b = 5 -> list.add(s);
```

#### 형식 추론

```java
// 형식을 추론하지 않음
Comparator<Apple> c = (Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());

// 형식을 추론함
Comparator<Apple> c = (a1, a2) -> a1.getWeight().compareTo(a2.getWeight());
```

#### 지역 변수 사용

-	람다 표현식에서는 익명 함수가 하는 것처럼 `자유변수`(파라미터로 넘겨진 변수가 아닌 외부에서 정의된 변수)를 활용할 수 있다. 이같은 동작은 `람다 캡처링`이라고 부른다.
-	하지만 final로 선언되어 있어야 하거나 실질적으로 final로 선언된 변수와 똑같이 사용되어야 한다.

### 메서드 레퍼런스

#### 요약

![메서드 레퍼런스-요약](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzRU0tWVpleU8wNk0)

#### 메서드 레퍼런스를 만드는 방법

1.	정적 메서드 레퍼런스
	-	Integer의 parseInt 메서드는 Integer::parseInt
2.	다양한 형식의 인스턴스 메서드 레퍼런스
	-	String의 length 메서드는 String::length
3.	기존 객체의 인스턴스 메서드 레퍼런스
	-	Transaction 객체에 getValue 메서드가 있다면, expensiveTransaction::getValue

![메서드 레퍼런스를 만드는 방법](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzbW9LLU9vMmFKNHc)

#### 생성자 레퍼런스

```java
Supplier<Apple> c1 = Apple::new;
Apple a1 = c1.get();

// 위 코드는 다음과 같다.
Supplier<Apple> c1 = () -> new Apple();
Apple a1 = c1.get();
```

```java
Function<Integer , Apple> c2 = Apple::new;
Apple a2 = c2 . apply(110);

Function<Integer, Apple> c2 = (weight) -> new Apple(weight);
Apple a2 = c2 . apply(110);
```
