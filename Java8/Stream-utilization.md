스트림 활용
-----------

### 필터링과 슬라이싱

#### 프레디케이트로 필터링

-	`filter` 메서드는 `프리디케이트`를 인수로 받아서 프레디케이트와 일치하는 모든 요소를 포함하느 스트림을 반환한다.

```java
List<Dish> vegetarianMenu =
                menu.stream()
                      .filter(Dish::isVegetarian)
                      .collect(toList());
```

![프레디케이트로 필터링](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzeDBOdjkzekZKdTA)

#### 고유 요소 필터링

-	스트림은 고유 요소로 이루어진 스트림을 반환하는 `distinct`라는 메서드도 지원한다.

```java
List<Integer> numbers = Arrays.asList(1, 2 ,1, 3, 3, 2, 4);
numbers.stream().filter (i -> i % 2 == 0)
                .distinct()
                .forEach(System.out::println);
```

![고유 요소 필터링](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzd2pqQWtKalp4Smc)

#### 스트림 축소

-	스트림은 주어진 사이즈 이하의 크기를 갖는 새로운 스트림을 반환하는 `limit(n)` 메서드를 지원한다.

```java
List<Dish> dishes = menu.stream()
                            .filter(d -> d.getCalories() > 300)
                            .limit(3)
                            .collect(toList());
```

![스트림 축소](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzcXFDcHBoZUtiYTg)

#### 요소 건너뛰기

-	스트림은 처음 n개 요소를 제외한 스트림을 반환하는 skip(n) 메서드를 지원한다.

```java
List<Dish> dishes = menu.stream()
                            .filter(d -> d.getCalories() > 300)
                            .skip(2)
                            .collect(toList());
```

### 매핑

-	SQL의 테이블에서 특정 열만 선택할 수 있다. 스트림 API의 map과 flatMap 메서드를 이용해 특정 데이터를 선택할 수 있다.

#### 스트림의 각 요소에 함수 적용하기

```java
// 요리명 추출하는 코드
List<Dish> dishes = menu.stream()
                            .map(Dish::getName)
                            .collect(toList());

// 요리명의 길이도 구하고  싶다면
List<Dish> wordLengths = menu.stream()
                                .map(Dish::getName)
                                .map(String::length)
                                .collect(toList());

```

#### 스트림 평면화

-	map과 Arrays.Stream 활용
-	flatMap 사용

```java
List<String> uniqueCharacters =
                  words.stream()
                          .map(w -> w.split(""))
                          .flatMap(Arrays::stream)
                          .distinct()
                          .collect(toList());
```

-	Stream<Stream[String]> 문제 해결을 위해 flatMap 사용.

![flatMap](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzLXcwaHZsMjNMYWM)

### 검색과 매칭

#### 프레디케이트가 적어도 한 요소와 일치하는지 확인

-	`anyMatch`를 이용한다. anyMatch는 불린을 반환하므로 최종 연산이다.

```java
if(menu.stream().anyMatch(Dish::isVegetarian)) {
  System.out.println("The menu is (somewhat) vegetarian friendly!!");
}
```

#### 프레디케이트가 모든 요소와 일치하는지 검사

-	`allMatch` 메서드는 anyMatch와 달리 스트림의 모든 요소가 주어진 프레디케이트와 일치하는지 검사한다.

```java
boolean isHealthy = menu.stream()
                            .allMatch(d -> d.getCalories() < 1000 );
```

#### noneMatch

-	allMatch 와 반대로 일치하는 요소가 없음을 확인한다.

```java
boolean isHealthy = menu.stream()
                            .noneMatch(d -> d.getCalories() >= 1000);
```

#### 요소 검색

-	`findAny` 메서드는 현재 스트림에서 임의의 요소를 반환한다. filter와 findAny를 이용해서 채식 요리를 선택할 수 있다.

```java
Optional<Dish> dish =
                 menu.stream()
                        .filter(Dish::isVegetarian)
                        .findAny();
```

#### 첫 번째 요소 찾기

-	`findFirst` 메서드 사용.

```java
List<Integer> someNumbers = Arrays.asList(1, 2, 3, 4, 5);
Optional<Integer> firstSquareDivisibleByThree =
                    someNumbers.stream()
                                  .map(x - > x * x)
                                  .filter(x - > x % 3 == 8)
                                  .findFirst(); // 9
```

> `findFirst`와 `findAny`는 일반적으로 결과과 같으나 병렬성 때문에 둘이 존재한다. 병렬 스트림에서는 제약이 없는 findAny를 사용한다.
