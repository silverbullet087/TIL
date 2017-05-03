새로운 날짜와 시간 API
----------------------

### LocalDate, LocalTime, Instant, Duration, Period

#### LocalDate와 LocalTime 사용

-	LocalDate 인스턴스는 시간을 제외한 날짜를 표현하는 불변 객체다.

```java
LocalDate date = LocalDate.of(2014, 3, 18);
int year = date.getYear(); // 2014
Month month = date.getMonth(); // MARCH
int day = date.getDayOfMonth(); // 18
DayOfWeek dow = date.getDayOfWeek(); // TUESDAY
int len = date.lengthOfMonth(); // 31 (days in March)
boolean leap = date.isLeapYear(); // false (not a leap year)
System.out.println(date);

int y = date.get(ChronoField.YEAR);
int m = date.get(ChronoField.MONTH_OF_YEAR);
int d = date.get(ChronoField.DAY_OF_MONTH);

```

-	시간은 LocalTime 클래스로 표현할 수 있다.

```java
LocalTime time = LocalTime.of(13, 45, 20); // 13:45:20
int hour = time.getHour(); // 13
int minute = time.getMinute(); // 45
int second = time.getSecond(); // 20
System.out.println(time);
```

-	날짜와 시간 문자열로 LocalDate와 LocalTime의 인스턴스를 만드는 방법도 있다.

```java
LocalDate date = LocalDate.parse("2014-03-18");
LocalTime time = LocalTime.parse("13:45:20");
```

#### 날짜와 시간 조합

-	`LocalDateTime`은 LocalDate와 LocalTime을 쌍으로 갖는 복합 클래스이다.

```java
LocalDateTime dt1 = LocalDateTime.of(2014, Month.MARCH, 18, 13, 45, 20); // 2014-03-18T13:45
LocalDateTime dt2 = LocalDateTime.of(date, time);
LocalDateTime dt3 = date.atTime(13, 45, 20);
LocalDateTime dt4 = date.atTime(time);
LocalDateTime dt5 = time.atDate(date);
System.out.println(dt1);
```

#### Instant: 기계의 날짜와 시간

-	Instant 클래스는 유닉스 에포크시간을 기준으로 특정 지점까지의 시간을 초로 표현한다.

```java
Instant instant = Instant.ofEpochSecond(44 * 365 * 86400);
Instant now = Instant.now();
```

#### Duration과 Period 정의

-	Duration 클래스의 정적 팩토리 메서드 between으로 두 시간 객체 사이의 `지속시간`을 만들 수 있다.

```java
Duration d1 = Duration.between(LocalTime.of(13, 45, 10), time);
Duration d2 = Duration.between(instant, now);
System.out.println(d1.getSeconds());
System.out.println(d2.getSeconds());
// 단 LocalDateTime은 사람이 사용하도록, Instant는 기계가 사용하도록 만들어진 클래스로 같이 사용할 수는 없다.
```

-	Period 클래스의 팩토리 메서드 between을 이용하면 두 LocalDate의 차이를 확인할 수 있다.

```java
Period tenDays = Period.between(LocalDate.of(2014, 3, 8), LocalDate.of(2014, 3, 18));
```

-	Duration과 Period 클래스가 공통으로 제공하는 메서드

![Duration과 Period 클래스가 공통으로 제공하는 메서드](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzei1DODh5ZGVPdjA)

### 날짜 조정, 파싱, 포매팅

-	withAttribute 메서드로 기존 LocalDate를 바꿀 수 있다.

```java
LocalDate date = LocalDate.of(2014, 3, 18);
date = date.withYear(2017);
date = date.withDayOfMonth(25);
date = date.with(ChronoField.MONTH_OF_YEAR);
```

-	지정된 시간을 추가하거나 뺄 수 있다.

```java
LocalDate date1 = LocalDate.of(2014, 3, 18);
// 2017-05-03
LocalDate date2 = date1.plusWeeks(1);
// 2017-05-10
LocalDate date3 = date2.minusYears(3);
// 2014-05-10
LocalDate date4 = date3.plus(6, ChronoUnit.MONTHS);
// 2014-11-10
```

-	특정 시점을 표현하는 날짜 시간 클래스의 공통 메서드

![특정 시점을 표현하는 날짜 시간 클래스의 공통 메서드](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzcWdpSUJmRXZIZzQ)
