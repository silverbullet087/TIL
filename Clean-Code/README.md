![Clean Code](http://drive.google.com/uc?export=view&id=0ByLqiEM75qEzazIwR3hELWQ3RGc)

-	책 제목 : Program, Programming, Programmer Clean Code 클린 코드 : 애자일 소프트웨어 장인 정신
-	저자 : 로버트 C. 마틴 저/박재호,이해영 공역 | 인사이트(insight)
-	http://www.yes24.com/24/goods/11681152?scode=032&OzSrank=1

-	**위의 책을 읽고 공부한 내용을 요약 정리한 것이다.**

목차
----

<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

-	[목차](#목차)
-	[깨끗한 코드](#깨끗한-코드)
	-	[나쁜코드](#나쁜코드)
	-	[나쁜 코드로 치르는 대가](#나쁜-코드로-치르는-대가)
	-	[태도](#태도)
	-	[깨끗한 코드란?](#깨끗한-코드란)
-	[의미 있는 이름](#의미-있는-이름)
	-	[의도를 분명히 밝혀라](#의도를-분명히-밝혀라)
	-	[그릇된 정보를 피하라](#그릇된-정보를-피하라)
	-	[의미 있게 구분하라](#의미-있게-구분하라)
	-	[발음하기 쉬운 이름을 사용하라](#발음하기-쉬운-이름을-사용하라)
	-	[검색하기 쉬운 이름을 사용하라](#검색하기-쉬운-이름을-사용하라)
	-	[인코딩을 피하라](#인코딩을-피하라)
	-	[자신의 기억력을 자랑하지 마라](#자신의-기억력을-자랑하지-마라)
	-	[클래스 이름](#클래스-이름)
	-	[메서드 이름](#메서드-이름)
	-	[한 개념에 한 단어를 사용하라](#한-개념에-한-단어를-사용하라)
	-	[말장난을 하지 마라](#말장난을-하지-마라)
	-	[해법 영역에서 가져온 이름을 사용하라](#해법-영역에서-가져온-이름을-사용하라)
	-	[문제 영역에서 가져온 이름을 사용하라](#문제-영역에서-가져온-이름을-사용하라)
	-	[의미 있는 맥락을 추가하라](#의미-있는-맥락을-추가하라)
	-	[불필요한 맥락을 없애라](#불필요한-맥락을-없애라)
-	[함수](#함수)
	-	[작게 만들어라](#작게-만들어라)
	-	[한가지만 해라](#한가지만-해라)
	-	[함수당 추상화 수준은 하나로!](#함수당-추상화-수준은-하나로)
	-	[위에서 아래로 코드 읽기: 내려가기 규칙](#위에서-아래로-코드-읽기-내려가기-규칙)
	-	[Switch문](#switch문)
	-	[서술적인 이름을 사용하라](#서술적인-이름을-사용하라)
	-	[함수 인수](#함수-인수)
	-	[부수 효과를 일으키지마라](#부수-효과를-일으키지마라)
	-	[명령과 조회를 분리하라](#명령과-조회를-분리하라)
	-	[오류 코드보다 예외를 사용하라](#오류-코드보다-예외를-사용하라)
	-	[반복하지마라](#반복하지마라)
	-	[함수를 어떻게 짜죠?](#함수를-어떻게-짜죠)
-	[주석](#주석)
	-	[주석은 나쁜 코드를 보완하지 못한다](#주석은-나쁜-코드를-보완하지-못한다)
	-	[코드로 의도를 표현하라](#코드로-의도를-표현하라)
	-	[좋은 주석](#좋은-주석)
	-	[나쁜 주석](#나쁜-주석)
-	[형식 마추기](#형식-마추기)
	-	[적절한 행 길이를 유지하라](#적절한-행-길이를-유지하라)
	-	[신문 기사처럼 작성하라](#신문-기사처럼-작성하라)
	-	[개념은 빈 행으로 분리하라](#개념은-빈-행으로-분리하라)
	-	[세로 밀집도](#세로-밀집도)
	-	[수직 거리](#수직-거리)
	-	[들여쓰기한다.](#들여쓰기한다)
	-	[팀 규칙을 지킨다.](#팀-규칙을-지킨다)
-	[객체와 자료 구조](#객체와-자료-구조)
	-	[자료/객체 비대칭](#자료객체-비대칭)
-	[오류 처리](#오류-처리)
	-	[오류 코드보다 예외를 사용하라](#오류-코드보다-예외를-사용하라-1)
	-	[Try-Catch-Finally 문부터 작성하라](#try-catch-finally-문부터-작성하라)
	-	[미확인 예외를 사용하라](#미확인-예외를-사용하라)
	-	[예외에 의미를 제공하라](#예외에-의미를-제공하라)
	-	[호출자를 고려해 예외 클래스를 정의하라](#호출자를-고려해-예외-클래스를-정의하라)
	-	[정상 흐름을 정의하라](#정상-흐름을-정의하라)
	-	[null을 반환하지마라](#null을-반환하지마라)
	-	[null을 전달하지마라](#null을-전달하지마라)
-	[경계(외부 API)](#경계외부-api)
	-	[외부 코드 사용하기](#외부-코드-사용하기)
	-	[경계 살피고 익히기](#경계-살피고-익히기)
	-	[log4j 익히기](#log4j-익히기)
	-	[학습 테스트는 공짜 이상이다.](#학습-테스트는-공짜-이상이다)
	-	[아직 존재하지 않는 코드를 사용하기](#아직-존재하지-않는-코드를-사용하기)
	-	[깨끗한 경계](#깨끗한-경계)
-	[단위 테스트](#단위-테스트)
	-	[TDD 법칙 세 가지](#tdd-법칙-세-가지)
	-	[깨끗한 테스트 코드 유지하기](#깨끗한-테스트-코드-유지하기)
	-	[테스트는 유연성, 유지보수성, 재사용성을 제공한다.](#테스트는-유연성-유지보수성-재사용성을-제공한다)
	-	[깨끗한 테스트 코드](#깨끗한-테스트-코드)
	-	[이중 표준](#이중-표준)
	-	[테스트 당 assert하나](#테스트-당-assert하나)
	-	[테스트 당 개념 하나](#테스트-당-개념-하나)
	-	[F.I.R.S.T](#first)
-	[클래스](#클래스)
	-	[클래스는 작아야 한다.](#클래스는-작아야-한다)
	-	[단일 책임 원칙](#단일-책임-원칙)
	-	[응집도](#응집도)
	-	[변하기 쉬운 클래스](#변하기-쉬운-클래스)
-	[시스템](#시스템)
	-	[시스템 제작과 시스템 사용을 분리하라](#시스템-제작과-시스템-사용을-분리하라)
-	[창발성](#창발성)
-	[동시성](#동시성)
-	[점진적인 개선](#점진적인-개선)
-	[냄새와 휴리스틱](#냄새와-휴리스틱)
	-	[주석](#주석-1)
	-	[환경](#환경)
	-	[함수](#함수-1)
	-	[일반](#일반)
	-	[자바](#자바)
	-	[이름](#이름)
	-	[테스트](#테스트)

<!-- tocstop -->

깨끗한 코드
-----------

### 나쁜코드

-	회사가 망한 원인은 바로 나쁜 코드 탓이었다.
-	우리 모두는 자신이 짠 쓰레기 코드를 쳐다보며 나중에 손보겠다고 생각한 경험이 있다. **나중은 결코 오지 않는다.**

### 나쁜 코드로 치르는 대가

-	나쁜 코드가 쌓일수록 팀 생산성은 떨어진다.
-	결국은 나쁜 코드를 더 많이 생산한다.
-	생산성은 더더욱 떨어져 거의 0이 된다.

### 태도

-	깨끗한 코드를 만드는 노력이 비용을 절감하는 방법일 뿐만 아니라 전문가로서 살아 남는 길이다.
-	나쁜 코드의 위험을 이해하지 못하는 관리자 말을 그대로 따르는 행동은 전문가답지 못하다.
-	기한을 맞추는 유일한 방법은 그러니까 빨리 가는 유일한 방법은, 언제나 코드를 깨끗하게 유지하는 습관인다.

### 깨끗한 코드란?

-	'코드 감각'이 있으면 좋은 코드와 나쁜코드를 구분한다. 그뿐만이 아니다. 절제와 규율을 적용해 나쁜 코드를 좋은 코드로 바쓰는 전략도 파악한다.
-	깨끗한 코드는 세세한 사항까지 꼼꼼하게 처리하는 코드다.
-	깨끗한 코드는 한가지에 '집중'한다.
-	깨끗한 코드는 잘 쓴 문장처럼 읽힌다.
-	깨끗한 코드란 다른 사람이 고치기 쉽다고 단언한다.
-	테스트 케이스가 없는 코드는 깨끗한 코드가 아니다. 아무리 코드가 우아해도 가독성이 높아도, 테스트 케이스가 없으면 깨끗하지 않다.
-	중복을 피하라. 한기능만 수행하라. 제대로 표현하라. 작게 추상화하라.
-	서둘러 끝내려면, 쉬게 짜려면, 읽기 쉽게 만들면 된다.

---

의미 있는 이름
--------------

### 의도를 분명히 밝혀라

### 그릇된 정보를 피하라

-	나름대로 널리 쓰이는 의미가 있는 단어를 다른 의미로 사용해선 안된다.
-	일관성이 떨어지는 표기법은 그릇된 정보다.

### 의미 있게 구분하라

-	읽는 사람이 차이를 알도록 이름을 지어라.

### 발음하기 쉬운 이름을 사용하라

### 검색하기 쉬운 이름을 사용하라

-	이름 길이는 범위 크기에 비례해야한다. 변수나 상수는 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 바람직하다.

### 인코딩을 피하라

### 자신의 기억력을 자랑하지 마라

-	문자 하나만 사용하는 변수 이름은 문제가 있다.
-	최악은 이미 a와 b는 사용하므로 c를 선택한다는 논리다.

### 클래스 이름

-	클래스 이름과 객체 이름은 명사나 명사구가 적합하다.

### 메서드 이름

-	메서드 이름은 동사나 동사구가 적합하다.접근자(get), 변경자(set), 조건자(is)

### 한 개념에 한 단어를 사용하라

-	추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.

### 말장난을 하지 마라

-	같은 맥락이 아닌데도 '일관성'을 고려해 add라는 단어를 선택해선 안된다.

### 해법 영역에서 가져온 이름을 사용하라

-	기술 개념에는 기술 이름이 가장 적합한 선택이다.

### 문제 영역에서 가져온 이름을 사용하라

### 의미 있는 맥락을 추가하라

-	이름에 맥락을 부여한다. 클래스를 만든 후 세 변수를 클래스에 넣었다 그러면 세 변수는 맥락이 분명해진다. 모든 방법이 실패하면 마지막 수단으로 접두어를 붙인다. Ex) addrFirstName, addrLastName.

### 불필요한 맥락을 없애라

-	일반적으로 짧은 이름이 긴 이름보다 좋다. 단, 의미가 분명한 경우에 한해서다.

---

함수
----

### 작게 만들어라

-	모든 함수가 2,3,4 줄로 만들어라. 각 함수가 이야기 하나를 표현한다.

### 한가지만 해라

-	함수는 한가지를 해야 한다. 그 한가지를 잘 해야 한다. 그 한 가지만을 해야한다.

### 함수당 추상화 수준은 하나로!

-	한 함수 내에 추상화 수준을 섞으면 코드를 읽는 사람이 헷갈린다.

	### 위에서 아래로 코드 읽기: 내려가기 규칙

-	코드는 위에서 아래로 이야기 처럼 읽혀야 좋다.

-	위에서 아래로 프로그램을 읽으면 함수 추상화 수준이 한번에 한단계씩 낮아진다.

-	To 문단을 읽듯이 프로그램이 읽혀야한다.

> To 입력 타입에 따라 입력 타입에 값을 일괄 수정한다.
>
> > To 입력 타입이 올바른지 체크한다.
> >
> > To 입력 타입에 맞는 일괄 수정값을 세팅한다.
> >
> > To 일괄 수정을 DB에 수정한다.

### Switch문

-	리팩토링기법을 이용하여 Switch문을 수정한다. 다형성 이용.

### 서술적인 이름을 사용하라

### 함수 인수

-	최선은 입력 인수가 없는 경우이며, 차선은 입력 인수가 1개뿐인 경우가.

### 부수 효과를 일으키지마라

### 명령과 조회를 분리하라

### 오류 코드보다 예외를 사용하라

### 반복하지마라

-	중복을 없앤다.

### 함수를 어떻게 짜죠?

-	처음에는 길고 복잡하다. 그런 다음 코드를 다듬고, 함수를 만들고 이름을 바꾸고, 중복을 제거한다. 메서드를 줄이고 순서를 바꾼다. 때로는 전체 클래스를 쪼갠다. 이와중에도 코드는 항상 단위 테스트를 통과한다.

---

주석
----

-	진실은 한곳에만 존재한다.
-	코드만이 정확한 정보를 제공하는 유일한 출처이다.
-	주석을 가능한 줄이도록 꾸준히 노력해야 한다.

### 주석은 나쁜 코드를 보완하지 못한다

### 코드로 의도를 표현하라

### 좋은 주석

-	법적인 주석
-	정보를 제공하는 주석

```java
// kk:mm:ss EEE, 매tJI dd, yyyy 형식이다.
Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

-	의도를 설명하는 주석
-	의미를 명료하게 밝히는 주석
-	결과를 경고하는 주석
-	TODO 주석
-	중요성을 강조하는 주석
-	공개 API에서 Javadocs

### 나쁜 주석

-	대다수 주석이 이 범주에 속한다.
-	주절거리는 주석
-	같은 이야기를 중복하는 주석
	-	코드내용을 그대로 중복설명
	-	코드를 정당화하는 주석도 아니고, 의도나 근거를 설명하는 주석도 아니고 코드보다 읽기가 쉽지 않은 주석
-	오해할 여지가 있는 주석
-	의무적으로 다는 주석
-	이력을 기록하는 주석
	-	예전엔 소스 코드 관리 시스템이 없었으니까 사용했으나 현재는 혼란만 가중시킨다.
-	있으나 마나한 주석
	-	너무 당연한 사실을 언급
-	무서운 잡음
	-	Javadocs도 잡음이다.
-	함수나 변수로 표현할 수 있다면 주석을 달지 마라
-	위치를 표시하는 주석
-	닫는 괄호에 다는 주석
-	공로를 돌리거나 저자를 표시하는 주석
-	주석으로 처리한 코드
	-	소그 코드 관리 시스템이 우리를 대신해 코드를 기억해준다.
-	HTML 주석
-	전역 정보
-	너무 많은 정보
-	모호한 관계
	-	주석과 주석이 설명하는 코드는 둘 사이 관계가 명확해야한다.
-	비공개 코드에서 Javadocs

---

형식 마추기
-----------

### 적절한 행 길이를 유지하라

### 신문 기사처럼 작성하라

### 개념은 빈 행으로 분리하라

-	빈 행은 새로운 개념을 시작한다는 시각적 단서다.

### 세로 밀집도

-	서로 밀집한 코드 행은 세로로 가까이 놓여야 한다.

### 수직 거리

-	변수는 사용하는 위치에 최대한 가까이 선언한다.
-	반면, 인스턴스 변수는 클래스 맨 처음에 선언한다.
-	한 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 배치한다.
-	친화도가 높을수록 코드를 가까이 배치한다.

### 들여쓰기한다.

### 팀 규칙을 지킨다.

---

객체와 자료 구조
----------------

### 자료/객체 비대칭

-	객체 지향 코드에서 어려운 변경은 절차적인 코드에서 쉬우며, 절차적인 코드에서 어려운 변경은 객체지향 코드에서 쉽다.
-	새로운 함수가 아닌 `새로운 자료 타입`이 필요한 경우 `클래스와 객체 지향 기법`이 적합하다.
-	반면, 새로운 자료 타입이 아닌라 `새로운 함수`가 필요한 경우 `절차적인 코드`가 적합하다.
-	모든 것이 객체라는 생각은 미신이다. 때로는 단순한 자료 구조와 절차적인 코드가 가장 적합한 상황도 있다.

---

오류 처리
---------

### 오류 코드보다 예외를 사용하라

### Try-Catch-Finally 문부터 작성하라

### 미확인 예외를 사용하라

-	확인된 예외가 반드시 필요하지 않다는 사실은 분명해졌다.
-	C#, C++, 파이썬, 루비등은 확인되 예외를 지원하지 않고 안정적인 소프트웨어를 구현하기에 무리가 없다.
-	오류가 치르는 비용에 상응하는 이익을 제공하는지 따져봐야 한다. 일반적인 애플리케이션은 의존성이라는 비용이 이익보다 크다.

### 예외에 의미를 제공하라

-	오류 메시지에 정보를 담아 예외와 함께 던진다.

### 호출자를 고려해 예외 클래스를 정의하라

-	예외 클래스를 사용한다.

### 정상 흐름을 정의하라

### null을 반환하지마라

### null을 전달하지마라

---

경계(외부 API)
--------------

### 외부 코드 사용하기

-	한 예로 java.util.Map이 제공하는 기능성과 유연성은 확실히 유용하지만 그만큼 위험도 크다.
-	Map 사용자라면 누구나 Map 내용을 지울 권한이 있다는 말이다.
-	마음만 먹으면 사용자는 어떤 객체 유형도 추가할 수 있다.
-	Map 인스턴스를 공개 API의 인수로 넘기거나 반환값으로 사용하지 않는다.

### 경계 살피고 익히기

-	간단한 테스트 케이스를 작성해 외부 코드를 익힌다.
-	학습 테스트는 API를 사용하려는 목적에 초점을 맞춘다.

### log4j 익히기

### 학습 테스트는 공짜 이상이다.

-	투자하는 노력보다 얻는 성과가 더 크다. 패키지 새 번전이 나온다면 학습 테스트를 돌려 차이가 있는지 확인한다.

### 아직 존재하지 않는 코드를 사용하기

-	ADAPTER 패턴으로 API 사용을 캡슐화래 API가 바뀔 때 수정할 코드를 한 곳으로 모은다.

### 깨끗한 경계

-	외부 패키지를 호출하는 코드를 가능한 줄여 경계를 관리한다. Map에서 봤듯이, 새로운 클래스로 경계를 감싸거나 아니면 ADAPTER 패턴을 사용해 우리가 원하는 인터페이스를 패키지가 제공하는 인터페이스로 변환한다. 어느 방법이든 코드 가독성이 높아지며, 경계 인터페이스를 사용하는 일관성도 높아지며, 외부 패키지가 변했을 때 변경할 코드도 줄어든다.

---

단위 테스트
-----------

### TDD 법칙 세 가지

1.	실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
2.	컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
3.	현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

### 깨끗한 테스트 코드 유지하기

-	테스트 코드는 실제 코드 못지 않게 중요하다.

### 테스트는 유연성, 유지보수성, 재사용성을 제공한다.

-	테스트 케이스가 있다면 공포는 사실상 사라진다.
-	테스트 케이스가 있으면 변경이 쉬워지기 때문이다.

### 깨끗한 테스트 코드

-	가독성은 실제 코드보다 테스트 코드에 더더욱 중요하다.

### 이중 표준

-	실제 환경에서는 절대로 안 되지만 테스트 환경에서는 전혀 문제없는 방식이 있다. 대개 메모리나 CPU 효율과 관련 있는 경우다. 코드의 깨끗함과는 철저히 무관하다.

### 테스트 당 assert하나

### 테스트 당 개념 하나

### F.I.R.S.T

-	F(Fast) : 테스트는 빨라야 한다.
-	I(Independent) : 각 테스트는 서로 의존하면 안 된다.
-	R(Repeatable) : 테스트는 어떤 환경에서도 반복 가능해야 한다.
-	S(Self-validating) : 테스트는 부울(boolean)값으로 결과를 내야한다. 성공 아니면 실패다.
-	T(Timely) : 테스트는 적시에 작성해야한다.

---

클래스
------

### 클래스는 작아야 한다.

-	클래스 이름은 해당 클래스 책임을 기술해야 한다.
-	클래스 설명은 만일("if"), 그리고("and"), -(하)며("or"), 하지만("but")을 사용하지 않고서 25단어 내외로 가능해야 한다.

### 단일 책임 원칙

-	단일 책임 원칙 : 클래스나 모듈은 변경할 이유가 하나, 단 하나뿐이어야 한다는 원칙이다.
-	클래스는 책임, 즉 변경할 이유가 하나여야 한다는 의미다.
-	큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이워진 시스템이 더 바람직하다.

### 응집도

-	응집도가 가장 높은 클래스는 가능하지도 바람직하지도 않다.
-	응집도를 유지하면서 작은 클래스 여럿이 나오게 한다.
	-	큰 함수를 작은 함수 여럿으로 쪼개다 보면 종종 작은 클래스 여럿으로 쪼갤 기회가 생긴다. 그러면서 프로그램에 점점 체계가 잡히고 구조다 투명해진다.

### 변하기 쉬운 클래스

-	새 기능을 수정하거나 기존 기능을 변경할 때 건드릴 코드가 최소인 시스템 구조가 바람직하다. 이상적인 시스템이라면 새 기능을 추가할 때 시스템을 확장 할 뿐 기존 코드를 변경하지 않는다.
-	변경으로부터 격리
	-	결합도가 낮다는 소리는 각 시스템 요소가 다른 요소로부터 그리고 변경으로부터 잘 격리되어 있다는 의미다.
	-	결합도를 최소로 줄이면 잘연스럽게 클래스가 상세한 규현이 아니라 추상화에 의존하게 된다.

---

시스템
------

### 시스템 제작과 시스템 사용을 분리하라

-	시스템 생성과 시스템 사용을 분리라는 한 가지 방법으로 생산과 관련한 코드는 모두 main이나 main이 호출하는 모듈로 옮기고, 애플리케이션은 생성한 객체를 사용한다.
-	사용과 제작을 분리하는 강력한 메커니즘 하나가 `의존성 주입`이다.
	-	스프링 프레임워크는 가장 널리 알려진 DI컨테이너를 제공한다. 객체 사이 의존성은 XML 파일에 정의한다. 그리고 자바 코드에서는 이름으로 특정한 객체를 요청한다.
-	확장
	-	처음부터 올바르게 시스템을 만들 수 있다는 믿음은 미신이다. 대신에 우리는 오늘 주어진 사용자 스토리에 맞춰 시스템을 구현해야 한다. 내일은 새로운 스토리에 맞춰 시스템을 조정하고 확장하면 된다. 이것이 반복적이고 점진적인 애자일 방식의 핵심이다. 테스트 주도 개발 TDD, 리팩토링, (TDD와 리팩터링으로 얻어지는) 깨끗한 코드는 코드 수준에서 시스템을 조정하고 확장하기 쉽게 만든다.
-	용어 정리

	-	영속성 : 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성을 의미한다.
	-	모듈화 : 규모가 큰 것을 여러 개로 나눈 조각, 하나 또는 몇 개의 논리적인 기능을 수행하기 위한 명령어들의 집합, 따라서 독립 프로그램도 하나의 모듈이 될 수 있고, 함수들도 하나의 모듈이 될 수 있다. 독립적인 기능을 갖는 단위(unit),
	-	관심사 : 보안, 로깅, 트랜젝션등과 같은 기능들
	-	황단 관심사 : 관심사가 한 애플리케이션의 여러부분에 걸쳐 있는 기능
	-	관점 : 여러 클레스에 걸친 관심사의 모듈화이다.

-	횡단 괌심사

	-	모듈화되고 캡슐화된 방식으로 영속성 방식을 구상한다. 영속성 방식을 구현한 코드가 온갖 객체로 흩어진다. 이런 것을 횡단 관심사라고 한다. `관점 지향 프로그래밍`(AOP)는 횡단 관심사에 대처해 모듈성을 확보하는 일반적인 방법론이다.

-	자바에서 사용하는 관점 혹은 관점과 유사한 메커니즘

	-	자바 프록시
	-	순수 자바 AOP 프레임워크
	-	AspectJ 관점

-	의사 결정을 최적화하라

	-	관심사를 모듈로 분리한 POJO 시스템은 기민함을 제공한다. 이런 기민함 덕택에 최신 정보에 기반해 최선의 시점에 최적의 결정을 내리기가 쉬워진다. 또한 결정의 복잡성도 줄어든다.

-	명백한 가치가 있을 때 표준을 현명하게 사용하라

	-	표준을 사용하면 아이디어와 컴포넌트를 재사용하기 쉽고, 적절한 경험을 가진 사람을 구하기 쉬우며, 좋은 아이디어를 캡슐화하기 쉽고, 컴포넌트를 엮기 쉽다. 하지만 때로는 표준을 만드는 시간이 너무 오래 걸려 업계가 기다리지 못한다. 어떤 표준은 원래 표준을 제정한 목적을 잊어버리기도 한다.

-	결론

	-	시스템 역시 깨끗해야 한다. 깨끗하지 못한 아키텍처는 도메인 노리를 흐리며 기민성이 떨어뜨린다. 도메인 노리가 흐려지면 제품 품질이 떨어진다. 버그가 숨어들기 쉬워지고, 스토리를 구현하기 어려워지는 탓이다. 기민성이 떨어지면 생산성이 낮아져 TDD가 제공하는 장점이 사라진다.
	-	모든 추상화 단계에서 의도는 명확히 표현해야 한다. 그러려면 POJO를 작성하고 관점 혹은 관점과 유사한 메커니즘을 사용해 각 구현 관심사를 분리해야한다.
	-	시스템을 설계하든 개별 모듈을 설게하든, 실제로 돌아가는 가장 단순한 수단을 사용해야 한다.

---

창발성
------

-	창발적 설계로 깔끔한 코드를 구현하자
	1.	모든 테스트를 실행하라
		-	테스트 케이스를 작성하면 설계 품질이 높아진다.
	2.	중복을 없애라
	3.	표현하라
		-	좋은 이름을 선택한다.
		-	함수와 클래스 크기를 가능한 줄인다.
		-	표준 명칭을 사용한다.
		-	단위 테스트 케이스를 꼼꼼히 작성한다.
	4.	클래스와 메서드 수를 최소로 줄여라
		-	함수와 클래스 크기를 작게 유지하면서 동시에 시스템 크기도 작게 유지하는데 있다. 하지만 우선순위가 가장 낮다.

---

동시성
------

-	다중 스레드 코드는 올바로 구현하기 어렵다.
-	스레드 코드는 최대한 집약되고 작아야 한다.
-	동시성 오류를 일으키는 잠정적인 원인을 철저히 이해한다.
-	사용하는 라이브러리와 기본 알고리즘을 이해한다.
-	보호할 코드 영역을 찾아내는 방법과 특정 코드 영역을 잠그는 방법을 이해한다.
-	스레드 코드는 많은 플랫폼에서 많은 설정으로 반복해서 계속 테스트해야 한다.

---

점진적인 개선
-------------

-	깨끗한 코드를 짜려면 먼저 지저분한 코드를 짠 뒤에 정리해야 한다.
	1.	코드를 짜다가 코드가 점점 엉망이 되어 간다.
	2.	계속 밀어붙이면 프로그램은 어떻게든 완성하겠지만 그랬다가는 넘무 커서 손대기 어려운 골칫거리가 생겨날 수 있다. 그래서 기능을 더이상 추가하지 않고 리팩터링을 시작한다.
	3.	점진적으로 개선한다. 리팩터링은 루빅 큐브 맞추기와 비슷한다. 큰 목표 하나를 이루기 위해 자잘한 단계를 수 없이 거친다. 각 단계를 거쳐야 다음 단계가 가능하다.
-	그저 돌아가는 코드만으로는 부족하다.
-	나쁜 코드보다 더 오랫동안 더 심각하게 개발 프로젝트에 악영향을 미치는 요인도 없다.
-	너무 서두르다가 이후로 영원히 자신들의 운명을 지배할 악성 코드라는 굴레를 짊어진다.
-	물론 나쁜 코드도 깨끗한 코드로 개선할 수 있다. 하지만 비용이 엄청나게 많이 든다.
-	반면 처음부터 코드를 깨끗하게 유지하기란 상대적으로 쉽다.얼마전에 엉망으로 만든 코드는 지금 당장 정리하기 아주 쉽다.
-	그러므로 코드는 언제나 최대한 깔끔하고 단순하게 정리해야한다. 절대로 썩어가게 방치하면 안 된다.

---

냄새와 휴리스틱
---------------

### 주석

-	부적절한 정보
	-	다른시스템(소스코드관리시스템 등)에 저장할 정보는 주석으로 적적하지 못하다.
-	쓸모 없는 주석
	-	오래된 잘못된 주석은 쓸모 없다.
-	중복된 주석
-	성의 없는 주석
-	주석 처리된 코드

### 환경

-	여러 단계로 빌드

	-	빌드는 간단히 한 단계로 끝나야 한다.

-	여러 단계로 테스트

	-	모든 단위 테스트는 한 명령으로 돌려야 한다.

### 함수

-	너무 많은 인수

-	죽은 함수

	-	아무도 호출하지 않는 함수는 삭제한다.

### 일반

-	한 소스 파일에 여러 언어를 사용하지 않는다.

-	당연한 동작을 구현하지 않는다.

	-	함수 기능을 직관적으로 예상하기 어렵다.

-	경계를 올바로 처리하지 않는다.

	-	모든 경계 조건을 찾아내고, 모든 경계 조건을 테스트하는 테스트 케이스를 작성한다.

-	안전 절차 무시

	-	실패하는 테스트 케이스를 일단 제껴두고 나중으로 미루면 안 된다.

-	중복

-	추상화 수준이 올바르지 못하다.

-	기초 클래스가 파생 클래스에 의존한다.

-	과도한 정보

	-	작을 수록 좋다.

-	죽은 코드

-	수직분리

	-	변수와 함수는 사용되는 위치에 가깝게 정의한다.

-	일관성 부족

	-	유사 개념은 동일 방식으로 구현한다.

-	잡동사니

	-	비어 있는 기본 생성자 같은 것은 작성하지 않는다.

-	기능 욕심

	-	클래스, 메서드는 자기 클래스의 변수와 함수에 관심을 가져야지 다른 클래스의 변수와 함수에 관심을 가져선 안 된다.

-	인위적 결합

	-	무관한 개념은 인위적으로 결합하지 않는다.

-	모호한 의도

-	부적절한 Static 함수

-	If/Else 혹은 Switch는 다형성을 사용해라.

-	표준 표기법을 따른다.

-	매직 숫자는 명명된 상수로 교체한다.

-	관례보단 구조를 사용한다.

-	함수는 한 가지만 해야한다.

-	일관성을 유지하라.

-	함수는 추상화 수준을 한 단계만 내려가야 한다.

-	추이적 탐색을 피하라

	-	일반적으로 한 모듈은 주변 모듈을 모를수록 좋다.

### 자바

-	상수는 상속하지 않는다.
-	상수 대신 Enum을 마음껏 활용하라.

### 이름

-	서술적인 이름을 사용하라
-	긴 범위는 긴 이름을 사용하라
-	인코딩을 피하라
-	이름으로 부수 효과를 설명하라

### 테스트

-	불충분한 테스트
	-	테스트 케이스는 잠재적으로 깨질 만한 부분을 모두 테스트해야한다.
-	사소한 테스트는 건너뛰지 마라
-	무시한 테스트는 모호함을 뜻한다.
-	경계 조건을 테스트하라
-	버그 주변은 철저히 테스트하라
-	실패 패턴을 살펴라
-	테스트 커버리지 패턴을 살펴라
-	테스트는 빨라야 한다.
