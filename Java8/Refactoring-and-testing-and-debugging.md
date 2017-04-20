리팩토링, 테스팅, 디버깅
------------------------

### 가독성과 유연성을 개선하는 리팩토링

#### 코드 가독성 개선

-	코드의 장황함을 줄여서 쉽게 이해할 수 있는 코드를 구현할 수 있다.
-	메서드 레퍼런스와 스트림 API를 이용해서 코드의 의도(코드가 무엇을 수행하려는 것인지)를 쉽게 표현할 수 있다.

#### 익명 클래스를 람다 표현식으로 리팩토링하기

-	람다 표현식을 이용해서 간결하고, 가독성이 좋은 코드를 구현할 수 있다. 하지만 익명 클래스를 람다 표현식으로 모두 변환할 수 있는 것은 아니다.
	1.	익명 클래스에서 사용한 this와 super는 람다 표현식에서 다른 의미를 갖는다. 익명 클래스에서 this는 익명 클래스 자신을 가리키지만 람다에서 this는 람다를 감싸는 클래스를 가리킨다.
	2.	익명 클래스는 감싸고 있는 클래스의 변수를 가릴 수 있다. 하지만 다음 코드에서 보여주는 것처럼 람다 표현식으로는 변수를 가릴 수 없다.

```java
int a = 10;
Runnable r1 = () -> {
  int a = 2; // 컴파일 에러
  System.out.println(a);
}

Runnable r2 = new Runnable () {
  public void run () {
    int a = 2; // 모든 것이 잘 동작
    System.out.println(a);
  }
}
```

#### 람다 표현식을 메서드 레퍼런스로 리팩토링하기

-	람다 표현식은 쉽게 전달할 수 있는 짧은 코드다. 하지만 람다 표현식 대신 메서드 레퍼런스를 이용하면 가독성을 높일 수 있다. 메서드 레퍼런스의 메서드명으로 코드의 의도를 명확하게 알릴 수 있기 때문이다.

#### 명령형 데이터 처리를 스트림으로 리팩토링하기

-	이론적으로는 반복자를 이용한 기존의 모든 컬렉션 처리 코드를 스트림 API로 바꿔야 한다. 스트림 API는 데이터 처리 파이프라인의 의도를 더 명확하게 보여준다.

```java
List<String> dishNames = new ArrayList<>();
for (Dish dish : menu) {
  if (dish.getCalories() > 300) {
    dishNames.add(dish.getName()) ;
  }
}

menu.parallelStream().
      .filter(d -> d.getCalories() > 300)
      .map(Dist::getName)
      .collect(toList());
```

#### 코드 유연성 개선

-	다양한 람다를 전달해서 다양한 동작을 표현할 수 있다. 따라서 변화하는 요구사항에 대응할 수 있는 코드르 구현할 수 있다.

### 람다로 객체지향 디자인 패턴 리팩토링하기

#### 전략

-	전략 패턴은 세부분으로 구성
	-	알고리즘을 나타내는 인터페이스(Strategy)
	-	다양한 알고리즘을 나타내는 한 개 이상의 인터페이스 구현
	-	전략 객체를 사용하는 한 개 이상의 클라이언트

![전략](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzaVp6Y183dHFHNk0)

-	java 8 이전 전략 패턴 코드

```java
interface ValidationStrategy {
    public boolean execute(String s);
}

static private class IsAllLowerCase implements ValidationStrategy {
    public boolean execute(String s){
        return s.matches("[a-z]+");
    }
}
static private class IsNumeric implements ValidationStrategy {
    public boolean execute(String s){
        return s.matches("\\d+");
    }
}

static private class Validator{
    private final ValidationStrategy strategy;
    public Validator(ValidationStrategy v){
        this.strategy = v;
    }
    public boolean validate(String s){
        return strategy.execute(s); }
}

// old school
Validator v1 = new Validator(new IsNumeric());
System.out.println(v1.validate("aaaa"));
Validator v2 = new Validator(new IsAllLowerCase ());
System.out.println(v2.validate("bbbb"));
```

-	**람다 표현식 사용**

```java
// with lambdas
Validator v3 = new Validator((String s) -> s.matches("\\d+"));
System.out.println(v3.validate("aaaa"));
Validator v4 = new Validator((String s) -> s.matches("[a-z]+"));
System.out.println(v4.validate("bbbb"));
```

#### 템플릿 메서드

-	알고리즘의 개요를 제시한 다음에 알고리즘의 일부를 고칠 수 있는 유연함을 제공해야 할 때 템플릿 메서드 디자인 패턴을 사용한다.

-	java 8 이전 전략 패턴 코드

```java
abstract class OnlineBanking {
    public void processCustomer(int id){
        Customer c = Database.getCustomerWithId(id);
        makeCustomerHappy(c);
    }
    abstract void makeCustomerHappy(Customer c);


    // dummy Customer class
    static private class Customer {}
    // dummy Datbase class
    static private class Database{
        static Customer getCustomerWithId(int id){ return new Customer();}
    }
}
```

-	**람다 표현식 사용**

```java
public class OnlineBankingLambda {

    public static void main(String[] args) {
        new OnlineBankingLambda().processCustomer(1337, (Customer c) -> System.out.println("Hello!"));
    }

    public void processCustomer(int id, Consumer<Customer> makeCustomerHappy){
        Customer c = Database.getCustomerWithId(id);
        makeCustomerHappy.accept(c);
    }

    // dummy Customer class
    static private class Customer {}
    // dummy Database class
    static private class Database{
        static Customer getCustomerWithId(int id){ return new Customer();}
    }
}
```

### 옵저버

-	어떤 이벤트가 발생했을 때 한 객체(주제라 불리는)가 다른 객체 리스트(옵저버라 불리는)에 자동으로 알림을 보내야 하는 상황에서 옵저버 디자인 패턴을 사용한다.

```java
public class ObserverMain {

    interface Observer{
        void inform(String tweet);
    }

    interface Subject{
        void registerObserver(Observer o);
        void notifyObservers(String tweet);
    }

    static private class NYTimes implements Observer{
        @Override
        public void inform(String tweet) {
            if(tweet != null && tweet.contains("money")){
                System.out.println("Breaking news in NY!" + tweet);
            }
        }
    }

    static private class Guardian implements Observer{
        @Override
        public void inform(String tweet) {
            if(tweet != null && tweet.contains("queen")){
                System.out.println("Yet another news in London... " + tweet);
            }
        }
    }

    static private class LeMonde implements Observer{
        @Override
        public void inform(String tweet) {
            if(tweet != null && tweet.contains("wine")){
                System.out.println("Today cheese, wine and news! " + tweet);
            }
        }
    }

    static private class Feed implements Subject{
        private final List<Observer> observers = new ArrayList<>();
        public void registerObserver(Observer o) {
            this.observers.add(o);
        }
        public void notifyObservers(String tweet) {
            observers.forEach(o -> o.inform(tweet));
        }
    }

}
```

-	java 8 이전 전략 패턴 코드

```java
public static void main(String[] args) {
    Feed f = new Feed();
    f.registerObserver(new NYTimes());
    f.registerObserver(new Guardian());
    f.registerObserver(new LeMonde());
    f.notifyObservers("The queen said her favourite book is Java 8 in Action!");
}
```

-	**람다 표현식 사용**

```java
public static void main(String[] args) {
    Feed feedLambda = new Feed();

    feedLambda.registerObserver((String tweet) -> {
        if(tweet != null && tweet.contains("money")){
            System.out.println("Breaking news in NY! " + tweet); }
    });
    feedLambda.registerObserver((String tweet) -> {
        if(tweet != null && tweet.contains("queen")){
            System.out.println("Yet another news in London... " + tweet); }
    });

    feedLambda.notifyObservers("Money money money, give me money!");

}
```

#### 의무 체인

-	작업처리 객체의 체인(동작 체인 등)을 만들 때는 의무 체인 패턴을 사용한다. 한 객체가 어떤 작업을 처리한 다음에 다른 객체로 결과를 전달하고, 다른 객체도 해야 할 작업을 처리한 다음에 또 다른 객체로 전달하는 식이다.
