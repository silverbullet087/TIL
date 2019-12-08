JPA 사용법
==========

목차
----

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

-	[1. Entity](#1-entity)
	-	[@Id](#id)
	-	[@GeneratedValue](#generatedvalue)
	-	[@Table](#table)
	-	[@Column](#column)
-	[2. Repository](#2-repository)
	-	[save](#save)
	-	[findOne](#findone)
	-	[findAll](#findall)
	-	[count](#count)
	-	[delete](#delete)
	-	[exists](#exists)
-	[3. 쿼리 작성 방법](#3-쿼리-작성-방법)
	-	[샘플소스](#샘플소스)
	-	[동작 SQL](#동작-sql)
	-	[쿼리 만드는 방법](#쿼리-만드는-방법)
	-	[기본예제](#기본예제)
-	[4. Pageable](#4-pageable)
	-	[호출 샘플소스](#호출-샘플소스)
-	[5. Entitiy간의 방향성](#5-entitiy간의-방향성)
-	[6. 양방향 연관관계의 주인](#6-양방향-연관관계의-주인)
-	[7. ManyToOne(N:1) 설정](#7-manytoonen1-설정)
-	[8. OneToMany(1:N) 설정](#8-onetomany1n-설정)
-	[9. OneToOne(1:1) 설정](#9-onetoone11-설정)
-	[10. JPA 프로그래밍: Fetch](#10-jpa-프로그래밍-fetch)

<!-- /code_chunk_output -->

### 1. Entity

#### @Id

-	primary key를 가지는 변수를 선언하는 것을 뜻한다.

#### @GeneratedValue

-	어노테이션은 해당 Id 값을 어떻게 자동으로 생성할지 전략을 선택할 수 있다.

#### @Table

-	별도의 이름을 가진 데이터베이스 테이블과 매핑한다. 기본적으로 @Entity로 선언된 클래스의 이름은 실제 데이터베이스의 테이블 명과 일치하는 것을 매핑한다. 따라서 @Entity의 클래스명과 데이터베이스의 테이블명이 다를 경우에 @Table(name=" ")과 같은 형식을 사용해서 매핑이 가능하다.

#### @Column

-	@Column 선언이 꼭 필요한 것은 아니다. 하지만 @Column에서 지정한 변수명과 데이터베이스의 컬럼명을 서로 다르게 주고 싶다면 @Column(name=" ") 같은 형식으로 작성하면 된다. 그렇지 않은 경우에는 기본적으로 멤버 변수명과 일치하는 데이터베이스 컬럼을 매핑한다.

### 2. Repository

```java
public interface CrudRepository<T, ID extends Serializable>
    extends Repository<T, ID> {

    <S extends T> S save(S entity);

    T findOne(ID primaryKey);       

    Iterable<T> findAll();          

    Long count();                   

    void delete(T entity);          

    boolean exists(ID primaryKey);  

    // … more functionality omitted.
}

```

#### save

-	레코드 저장 (insert, update)

#### findOne

-	primary key로 레코드 한건 찾기

#### findAll

-	전체 레코드 불러오기. 정렬(sort), 페이징(pageable) 가능

#### count

-	레코드 갯수

#### delete

-	레코드 삭제

#### exists

-	존재여부

### 3. 쿼리 작성 방법

#### 샘플소스

```java
public interface UserRepository extends Repository<User, Long> {

  List<User> findByEmailAddressAndLastname(String emailAddress, String lastname);
}
```

#### 동작 SQL

```SQL
select u from User u where u.emailAddress = ?1 and u.lastname = ?2
```

#### 쿼리 만드는 방법

-	리턴타입 {접두어}{도입부}By{프로퍼티 표현식}(조건식)[(And|Or){프로퍼티 표현식}(조건식)]{정렬 조건} (매개변수)

| 각부분          | 매소드명                                                        |
|:----------------|:----------------------------------------------------------------|
| 접두어          | Find, Get, Query, Count, ...                                    |
| 도입부          | Distinct, First(N), Top(N)                                      |
| 프로퍼티 표현식 | Person.Address.ZipCode => find(Person)ByAddress_ZipCode(...)    |
| 조건식          | IgnoreCase, Between, LessThan, GreaterThan, Like, Contains, ... |
| 정렬 조건       | OrderBy{프로퍼티}Asc                                            |
| 리턴 타입       | E, Optional<E>, List<E>, Page<E>, Slice<E>, Stream<E>           |
| 매개변수        | Pageable, Sort                                                  |

-	지원하는 쿼리 키워드 메소드명

| Keyword           | Sample                                                  | JPQL snippet                                                   |
|:------------------|:--------------------------------------------------------|:---------------------------------------------------------------|
| And               | findByLastnameAndFirstname                              | … where x.lastname = ?1 and x.firstname = ?2                   |
| Or                | findByLastnameOrFirstname                               | … where x.lastname = ?1 or x.firstname = ?2                    |
| Is,Equals         | findByFirstname,findByFirstnameIs,findByFirstnameEquals | … where x.firstname = ?1                                       |
| Between           | findByStartDateBetween                                  | … where x.startDate between ?1 and ?2                          |
| LessThan          | findByAgeLessThan                                       | … where x.age < ?1                                             |
| LessThanEqual     | findByAgeLessThanEqual                                  | … where x.age ⇐ ?1                                             |
| GreaterThan       | findByAgeGreaterThan                                    | … where x.age > ?1                                             |
| GreaterThanEqual  | findByAgeGreaterThanEqual                               | … where x.age >= ?1                                            |
| After             | findByStartDateAfter                                    | … where x.startDate > ?1                                       |
| Before            | findByStartDateBefore                                   | … where x.startDate < ?1                                       |
| IsNull            | findByAgeIsNull                                         | … where x.age is null                                          |
| IsNotNull,NotNull | findByAge(Is)NotNull                                    | … where x.age not null                                         |
| Like              | findByFirstnameLike                                     | … where x.firstname like ?1                                    |
| NotLike           | findByFirstnameNotLike                                  | … where x.firstname not like ?1                                |
| StartingWith      | findByFirstnameStartingWith                             | … where x.firstname like ?1 (parameter bound with appended %)  |
| EndingWith        | findByFirstnameEndingWith                               | … where x.firstname like ?1 (parameter bound with prepended %) |
| Containing        | findByFirstnameContaining                               | … where x.firstname like ?1 (parameter bound wrapped in %)     |
| OrderBy           | findByAgeOrderByLastnameDesc                            | … where x.age = ?1 order by x.lastname desc                    |
| Not               | findByLastnameNot                                       | … where x.lastname <> ?1                                       |
| In                | findByAgeIn(Collection<Age> ages)                       | … where x.age in ?1                                            |
| NotIn             | findByAgeNotIn(Collection<Age> age)                     | … where x.age not in ?1                                        |
| TRUE              | findByActiveTrue()                                      | … where x.active = true                                        |
| FALSE             | findByActiveFalse()                                     | … where x.active = false                                       |
| IgnoreCase        | findByFirstnameIgnoreCase                               | … where UPPER(x.firstame) = UPPER(?1)                          |

#### 기본예제

```java
//기본 예제

List<Person> findByEmailAddressAndLastname(EmailAddress emailAddress, String lastname);
// distinct
List<Person> findDistinctPeopleByLastnameOrFirstname(String lastname, String firstname);
List<Person> findPeopleDistinctByLastnameOrFirstname(String lastname, String firstname);
// ignoring case
List<Person> findByLastnameIgnoreCase(String lastname);
// ignoring case
List<Person> findByLastnameAndFirstnameAllIgnoreCase(String lastname, String firstname);

//정렬

List<Person> findByLastnameOrderByFirstnameAsc(String lastname);
List<Person> findByLastnameOrderByFirstnameDesc(String lastname);

//페이징

Page<User> findByLastname(String lastname, Pageable pageable);
Slice<User> findByLastname(String lastname, Pageable pageable);
List<User> findByLastname(String lastname, Sort sort);
List<User> findByLastname(String lastname, Pageable pageable);


```

### 4. Pageable

#### 호출 샘플소스

```java
@Controller
@RequestMapping("/users")
public class UserController {

  @Autowired UserRepository repository;

  @RequestMapping
  public String showUsers(Model model, Pageable pageable) {

    model.addAttribute("users", repository.findAll(pageable));
    return "users";
  }
}
```

-	위와 같이 작성된 Pageable에서는 다음과 같은 파라미터를 자동 수집한다.

| parameter | Header Two                                              |
|:----------|:--------------------------------------------------------|
| page      | 페이지 인지를 전달(0부터 시작)                          |
| size      | 한 페이지 사이즈(기본값 20)                             |
| sort      | 정렬정보를 전달. 예:sort=createdAt,desc&sort=userId,asc |

### 5. Entitiy간의 방향성

-	A클래스는 B클래스를 사용하게 되고 이런 경우에 방향성을 갖습니다. 반대로 B클래스가 A클래스를 사용하게 되면 역시 방향성을 갖습니다.
-	가능한 단방향만으로 구현을 해보고 양방향이 필요한 경우에 성능과 편의성을 고려하여서 양방향을 추가하는 방식이 좋습니다.

### 6. 양방향 연관관계의 주인

-	두 개의 Entity 클래스가 양방향으로 서로 참조를 하고 있으면, '연관관계의 주인'을 지정해줘야 합니다.
-	연관관계의 주인만이 외래키를 관리하여 갱신(등록, 수정, 삭제)를 할 수 있고, 반대편은 읽기만 가능하도록 만들기 위함입니다. 연관관계의 주인은 FK(외래키)가 명시된 Entity클래스로 설정합니다. (쉽게말해 mappedBy라는 옵션을 사용하는 쪽은 주인이 아닙니다).

### 7. ManyToOne(N:1) 설정

-	다대일 설정시의 FK(외래키)는 N(Many)쪽에 둡니다.

![n:1](http://drive.google.com/uc?export=view&id=1Pv3TYwlof4qVhjVe96thKxQcEE76j0S-)

### 8. OneToMany(1:N) 설정

-	다대일 설정시의 FK(외래키)는 N(Many)쪽에 둡니다. 하지만 N(Many)쪽에서 단방향 참조를 하고 있지 않으면 FK(외래키)설정할 필드값이 존재하지 않습니다. 그러므로 FK(외래키) 설정은 1(One)쪽에서 설정합니다. 양방향 설정을 하기 위해서는 ManyToOne의 양방향 구현방식을 사용합니다.

![1:n](http://drive.google.com/uc?export=view&id=1zk-_M_K-TMigTMGr-WARW84TGxEzwfJ4)

### 9. OneToOne(1:1) 설정

-	일대일 관계에서는 '주(主)테이블'을 정해야 합니다. 주테이블이라는 것은 단독적으로도 사용가능한 테이블을 말합니다. (혹은 기획상의 확장성을 고려해서 주테이블을 결정하기도 합니다.) 아래표에서는 왼쪽열이 주테이블, 오른쪽열이 대상테이블 입니다. 참고로 대상테이블에 외래키가 있는 단방향은 구현할 수 없습니다.

![1:1](http://drive.google.com/uc?export=view&id=1dCbF8VWHi-K1k6b4gbFiSUQaKo2nezNc)

-	[출처 : 양방향 관계 표 - siyoon210 블로그 - JPA Entity간의 연관관계(방향) 설정하기](https://siyoon210.tistory.com/27)

### 10. JPA 프로그래밍: Fetch

-	@OneToMany의 기본값은 Lazy
-	@ManyToOne의 기본값은 Eager
