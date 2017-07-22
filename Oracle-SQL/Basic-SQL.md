Basic SQL
=========

---

-	출처 : 구루비 강좌 - http://www.gurubee.net/oracle/sql
-	구루비사이트 강좌를 마크다운 형식으로 정리하면서 공부를 하였습니다.

<!-- @import "[TOC]" {cmd:"toc", depthFrom:1, depthTo:6, orderedList:false} -->

<!-- code_chunk_output -->

-	[1. SQL의 종류](#1-sql의-종류)
-	[2. USER의 생성과 권한의 설정](#2-user의-생성과-권한의-설정)
	-	[2.1. USER의 생성](#21-user의-생성)
	-	[2.2. USER의 변경 및 삭제](#22-user의-변경-및-삭제)
	-	[2.3. 권한과 롤](#23-권한과-롤)
		-	[2.3.1. 시스템 권한(System Privileges)](#231-시스템-권한system-privileges)
		-	[2.3.2. 객체 권한(Object Privileges)](#232-객체-권한object-privileges)
		-	[2.3.3. 롤(Role)](#233-롤role)
		-	[2.3.4. 오라클 데이터베이스를 설치하면 기본적으로 생성되는 Role](#234-오라클-데이터베이스를-설치하면-기본적으로-생성되는-role)
-	[3. 테이블의 생성과 수정 그리고 삭제](#3-테이블의-생성과-수정-그리고-삭제)
	-	[3.1. 테이블의 생성](#31-테이블의-생성)
	-	[3.2. 테이블의 제약조건](#32-테이블의-제약조건)
	-	[3.3. 오라클 데이터 타입](#33-오라클-데이터-타입)
	-	[3.4. LOB, LONG, LONG RAW 데이터 타입 간의 비교](#34-lob-long-long-raw-데이터-타입-간의-비교)
	-	[3.5. 테이블의 관리](#35-테이블의-관리)
-	[4. 데이터 조작어(DML)](#4-데이터-조작어dml)
	-	[4.1. 데이터의 삽입, 수정, 삭제](#41-데이터의-삽입-수정-삭제)
		-	[4.1.1. MERGE 문의 이해 및 활용](#411-merge-문의-이해-및-활용)
	-	[4.2. SELECT문 및 연산자](#42-select문-및-연산자)
	-	[4.3. 예명(Alias)](#43-예명alias)
	-	[4.4. 조인(Join)](#44-조인join)
		-	[4.4.1. Equi Join, Non_Equi Join, Self Join](#441-equi-join-non_equi-join-self-join)
		-	[4.4.2. Outer Join (LEFT, RIGHT, FULL OUTER JOIN)](#442-outer-join-left-right-full-outer-join)
		-	[4.4.3. CROSS JOIN, INNER JOIN, NATURAL JOIN, USING, ON](#443-cross-join-inner-join-natural-join-using-on)
	-	[4.5. 트랜잭션(commit과 rollback)](#45-트랜잭션commit과-rollback)
	-	[4.6. Commit과 Rollback 예제](#46-commit과-rollback-예제)
-	[5. 내장 함수(Sing-Row Functions)](#5-내장-함수sing-row-functions)
	-	[5.1. Numeric Functions (숫자형 함수)](#51-numeric-functions-숫자형-함수)
	-	[5.2. Character Functions (문자형 함수)](#52-character-functions-문자형-함수)
	-	[5.3. Datetime Functions (날짜 함수)](#53-datetime-functions-날짜-함수)
	-	[5.4. Conversion Functions (변환 함수)](#54-conversion-functions-변환-함수)
	-	[5.5. 기타 함수들](#55-기타-함수들)
	-	[5.6. DECODE와 CASE](#56-decode와-case)
	-	[5.7. NVL, NVL2, NULLIF, COALESCE](#57-nvl-nvl2-nullif-coalesce)
-	[6. 집계함수(Aggregate function)의 이해](#6-집계함수aggregate-function의-이해)
	-	[6.1. 집계함수(Aggregate function)란?](#61-집계함수aggregate-function란)
	-	[6.2. GROUP BY와 HAVING절](#62-group-by와-having절)
-	[7. 서브쿼리(Subquery)](#7-서브쿼리subquery)
	-	[7.1. Subquery란?](#71-subquery란)
	-	[7.2. Single-Row Subquery](#72-single-row-subquery)
	-	[7.3. Multiple-Row Subquery](#73-multiple-row-subquery)
	-	[7.4. Multiple-Column Subquery](#74-multiple-column-subquery)
	-	[7.5. Inline View (From절 Subquery)](#75-inline-view-from절-subquery)
	-	[7.6. Scalar Subquery](#76-scalar-subquery)
	-	[7.7. UNION [ALL], INTERSECT, MINUS 연산자](#77-union-all-intersect-minus-연산자)
-	[8. 데이터 사전 (Data Dictionary)](#8-데이터-사전-data-dictionary)
	-	[8.1. 데이터 사전(Data Dictionary)이란?](#81-데이터-사전data-dictionary이란)
	-	[8.2. 데이터 사전(Data Dictionary) 정보조회](#82-데이터-사전data-dictionary-정보조회)
-	[9. 오라클 객체](#9-오라클-객체)
	-	[9.1. 인덱스(Index)](#91-인덱스index)
	-	[9.2. VIEW 테이블](#92-view-테이블)
	-	[9.3. 시퀀스(Sequence)의 이해 및 활용](#93-시퀀스sequence의-이해-및-활용)
	-	[9.4. SYNONYM(동의어)](#94-synonym동의어)

<!-- /code_chunk_output -->

### 1. SQL의 종류

1.	**DDL(Date Definition Language)** : 데이터베이스 객체(테이블, 뷰, 인덱스..)의 구조를 정의 한다.

| SQL문  | 내용                                                           |
|:-------|:---------------------------------------------------------------|
| Create | 데이터베이스 객체를 생성한다.                                  |
| DROP   | 데이터베이스 객체를 삭제한다.                                  |
| ALTER  | 기존에 존재하는 데이터베이스 객체를 다시 정의하는 역할을 한다. |

1.	**DML(Data Manipulation Language)** : 데이터의 삽입, 삭제, 갱신 등의 처리한다.

| SQL문  | 내용                                   |
|:-------|:---------------------------------------|
| INSERT | 데이버베이스 객체에 데이터를 입력한다. |
| DELETE | 데이터베이스 객체의 데이터를 삭제한다. |
| UPDATE | 데이터베이스 객체안의 데이터 수정한다. |

1.	**DCL(Data Control Language)** : 데이터베이스 사용자의 권한을 제어한다.

| SQL문  | 내용                                           |
|:-------|:-----------------------------------------------|
| GRANT  | 데이터베이스 객체에 권한을 부여한다.           |
| REVOKE | 이미 부여된 데이터베이스 객체 권한을 취소한다. |

### 2. USER의 생성과 권한의 설정

#### 2.1. USER의 생성

-	새로운 USER를 생성하기 위해서는 CREATE USER문을 이용하면 된다.
-	USER를 생성하기 위해서는 USER 생성 권한이 있는 사용자로 접속해야한다.

![USER의 생성](http://www.gurubee.net/imgs/oracle/sql/CreateUser.jpg)

-	user_name : USER 이름
-	BY password : USER가 데이터베이스에 의해 인증되도록 지정하며, 데이터베이스 USER 로그인시 사용하는 비밀번호 이다.
-	EXTERNALLY : USER가 운영 체제에 의해서 인증되도록 지정한다.
-	DEFAULT TABLESPACE는 USER 스키마를 위한 기본 테이블스페이스를 지정 한다.
-	TEMPORARY TABLESPACE는 USER의 임시 테이블스페이스를 지정한다.
-	QUOTA절을 사용하여 USER가 사용할 테이블스페이스의 영역을 할당한다.
-	PASSWORD EXPIRE : USER가 SQL*PLUS를 사용하여 데이터베이스에 로그인할 때 암호를 재설정 하도록 한다.(USER가 데이터베이스에 의해 인증될 경우에만 적합한 옵션이다.)
-	ACCOUNT LOCK/UNLOCK : USER 계정을 명시적으로 잠그거나 풀 때 사용할 수 있다.(UNLOCK이 기본값이다.)
-	PROFILE : 자원 사용을 제어하고 USER에게 사용되는 암호 제어 처리 방식을 지정하는데 사용된다. 여기선 간단한 유저생성에 대해서만 알아보고 자세한 유저관리와 PROFILE 관리는 어드민에서 설명 하겠다.

**※ 참고 1**

-	임시 테이블스페이스를 지정해 주지 않으면 시스템 테이블스페이스가 기본으로 지정 되지만, 시스템 테이블스페이스에 단편화가 발생할 수 있으므로 USER를 생성할때 임시테이블스페이스를 따로 지정해 주는 것이 좋다.

-	또한 DEFAULT TABLESPACE도 USER를 생성할때 지정해 주지 않으면 기본적으로 시스템 테이블스페이스가 지정이 된다. 하지만 USER를 생성할때 DEFAULT TABLESPACE를 지정을 해서 USER가 소유한 데이터와 객체들의 저장 공간을 별도로 관리를 해야 한다.

-	시스템 테이블스페이스는 본래의 목적(모든 데이터 사전 정보와, 저장 프로시저, 패키지, 데이터베이스 트리거등을 저장)을 위해서만 사용되어져야 하지 일반USER의 데이터 저장용으로 사용 되어서는 안된다.

**참고 2, 테이블스페이스란?**

-	오라클 서버가 데이터를 저장하는 논리적인 구조이다.
-	테이블스페이스는 하나 또는 여러개의 데이터 파일로 구성되는 논리적인 데이터 저장 구조이다.

**USER 생성 예제**

```SQL
-- SQL PLUS를 싱행시키고 SCOTT/TIGER로 접속한다.
CREATE USER TEST IDENTIFIED BY TEST;
1행에 오류: ORA-01031: 권한이 불충분합니다


-- SCOTT USER는 사용자 생성 권한이 없어서 사용자를 생성할 수 없다.
-- DBA Role이 있는 유저로 접속
-- sqlplus / as sysdba 로 접속하셔도 됩니다.

SQL>CONN sys/manager AS SYSDBA

CREATE USER TEST IDENTIFIED BY TEST;

-- 새로 생성한 USER로 접속
SQL> CONN TEST/TEST

ERROR:
ORA-01045: 사용자 TEST는 CREATE SESSION 권한을 가지고있지 않음;

-- 새로 생성한 TEST USER는 권한이 없어서 접근할 수가 없다.
-- 모든 USER는 권한이 있고 권한에 해당하는 역할만 할 수 있다.
-- TEST라는 USER를 사용하기 위해서도 권한을 부여해 주어야 한다.

SQL>CONN sys/manager AS SYSDBA
연결되었습니다.

GRANT connect, resource TO TEST ;
권한이 부여되었습니다.

SQL> CONN TEST/TEST
연결되었습니다.
```

#### 2.2. USER의 변경 및 삭제

**ALTER USER문으로 변경 가능한 옵션**

-	비밀번호
-	운영체제 인증
-	디폴트 테이블 스페이스
-	임시 테이블 스페이스
-	프로파일 및 디폴트 역할

**USER 수정 문법**

![USER 수정 문법](http://www.gurubee.net/imgs/oracle/sql/AlterUser.jpg)

**USER 수정 예제**

```SQL
-- SYS 권한으로 접속한다.
C:\> SQLPLUS /NOLOG
CONN / AS SYSDBA

-- scott USER의 비밀번호를 수정한다.
ALTER USER scott IDENTIFIED by lion;
사용자가 변경되었습니다.

-- scott USER의 비밀번호가 변경된 것을 확인할 수 있다.
CONN scott/lion
접속되었습니다.

CONN / AS SYSDBA
접속되었습니다.

-- scott USER의 비밀번호를 처음처럼 수정한다.
alter USER scott IDENTIFIED by tiger;
사용자가 변경되었습니다.
```

<br/>

**USER 삭제 예제**

![USER 삭제 예제](http://www.gurubee.net/imgs/oracle/sql/DropUser.jpg)

CASECADE를 사용하게 되면 사용자 이름과 관련된 모든 데이터베이스 스키마가 데이터 사전으로부터 삭제되며 모든 스키마 객체들 또한 물리적으로 삭제 된다.

**USER 정보의 확인**

```SQL
-- 데이터베이스에 등록된 사용자를 조회하기 위해서는 DBA_USERS라는
    데이터사전을 조회하면 된다.
-- SQL*Plus를 실행시켜  SYS계정으로 접속을 한다.
SQL> CONN / AS SYSDBA

SQL> SELECT username, default_tablespace, temporary_tablespace
     FROM DBA_USERS;

USERNAME         DEFAULT_TABLESPACE      TEMPORARY_TABLES
---------------- -------------------     ----------------
SYS               SYSTEM                  TEMP
SYSTEM            TOOLS                   TEMP
OUTLN             SYSTEM                  SYSTEM
DBSNMP            SYSTEM                  SYSTEM
ORDSYS            SYSTEM                  SYSTEM
ORDPLUGINS        SYSTEM                  SYSTEM
MDSYS             SYSTEM                  SYSTEM
CTXSYS            DRSYS                   DRSYS
SCOTT             SYSTEM                  SYSTEM
TEST              TEST                    SYSTEM
STORM             STORM                   SYSTEM
KJS               SYSTEM                  SYSTEM

 위와 같이 유저와 테이블 스페이스에 대한 정보가 화면에 나온다.    
```

#### 2.3. 권한과 롤

##### 2.3.1. 시스템 권한(System Privileges)

오라클에서 권한(Privilege)은 특정 타입의 SQL문을 실행하거나 데이터베이스나 객체에 접근할 수 있는 권리이다.

**시스템권한(System Privileges)이란?**

-	시스템권한은 사용자가 데이터베이스에서 특정 작업을 수행 할 수 있도록 한다.
-	권한의 ANY 키워드는 사용자가 모든 스키마에서 권한을 가짐을 의미한다.
-	GRANT 명령은 사용자 또는 ROLE에 대해서 권한을 부여 할 수 있다.
-	REVOKE 명령은 권한을 회수 한다.

**대표적인 시스템권한**

-	CREATE SESSION : 데이터베이스를 연결할 수 있는 권한
-	CREATE ROLE : 오라클 데이터베이스 역할을 생성할 수 있는 권한
-	CREATE VIEW : 뷰의 생성권한
-	ALTER USER : 생성한 사용자의 정의를 변경할 수 있는 권한
-	DROP USER : 생성한 사용자를 삭제시키는 권한

**시스템권한 부여 문법**

![시스템권한 부여 문법](http://www.gurubee.net/imgs/oracle/sql/S_Privilege.jpg)

-	system-privilege : 부여할 시스템 권한의 이름
-	role : 부여할 데이터베이스 역할의 이름
-	user, role : 부여할 사용자 이름과 다른 데이터베이스 역할의 이름
-	PUBLIC : 시스템권한, 또는 데이터베이스 역할을 모든 사용자에게 부여할 수 있다.
-	WITH ADMIN OPTION : 권한을 부여 받은 사용자도 부여 받은 권한을 다른 사용자 또는 역할로 부여할 수 있게된다.

**시스템권한 부여 예제**

```SQL
-- SYS 권한으로 접속한다.   
SQL>CONN sys/manager AS SYSDBA

-- scott 사용자에게 사용자를 생성, 수정, 삭제 할 수 있는 권한을 부여하고,
-- scott 사용자도 다른 사용자에게 그 권한을 부여 할 수 있도록 권한 부여.
SQL>GRANT CREATE USER, ALTER USER, DROP USER TO scott WITH ADMIN OPTION;
 권한이 부여되었습니다.
```

<br/>

**시스템권한의 회수**

![시스템권한의 회수](http://www.gurubee.net/imgs/oracle/sql/S_Revoke.jpg)

**시스템권한 회수 예제**

```SQL
-- scott 사용자에게 부여한 생성, 수정, 삭제 권한을 회수 한다.
REVOKE CREATE USER, ALTER USER, DROP USER
FROM scott;
권한이 회수되었습니다.
```

**WITH ADMIN OPTION을 사용하여 시스템권한 취소**

WITH ADMIN OPTION을 사용하여 시스템권한을 부여했어도 시스템권한을 취소할 때는 연쇄적으로 취소 되지 않는다.

시나리오

1.	DBA가 STORM에게WITH ADMIN OPTION을 사용하여 CREATE TABLE 시스템권한을 부여 한다.
2.	STORM이 테이블을 생성 한다.
3.	STORM이 CREATE TABLE 시스템권한을 SCOTT에게 부여 한다.
4.	SCOTT가 테이블을 생성 한다.
5.	DBA가 STORM에게 부여한 CREATE TABLE 시스템권한을 취소 한다.

![시나리오](http://www.gurubee.net/imgs/oracle/sql/WithAdminOption.jpg)

결과

-	STORM의 테이블은 여전히 존재하지만 새 테이블을 생성할 수 있는 권한은 없다.
-	SCOTT는 여전히 테이블과 새로운 테이블을 생성 할 수 있는 CREATE TABLE권한을 가지고 있다.

![결과](http://www.gurubee.net/imgs/oracle/sql/WithAdminOption2.jpg)

##### 2.3.2. 객체 권한(Object Privileges)

객체권한은 USER가 소유하고 있는 특정 객체를 다른 사용자들이 엑세스 하거나 조작 할 수 있게 하기 위해 생성한다.

**객체권한(Object Privileges) 이란**

-	테이블이나 뷰, 시퀀스, 프로시저, 함수, 또는 패키지 중 지정된 한 객체에 특별한 작업을 수행 할 수 있게 한다.
-	객체 소유자는 다른 사용자에게 특정 객체권한을 부여할 수 있다.
-	PUBLIC 으로 권한을 부여하면 회수할 때도 PUBLIC으로 해야 한다.
-	기본적으로 소유한 객체에 대해서는 모든 권한이 자동적으로 획득된다.
-	WITH ADMIN OPTION 옵션은 ROLE에 권한을 부여할 때는 사용할 수 없다.

**객체에 따른 권한 목록 예**

| 객체권한 | 테이블 | 뷰 | 시퀀스 | 프로시저 |
|:---------|:-------|:---|:-------|:---------|
| ALTER    | ○      |    | ○      |          |
| DELETE   | ○      | ○  |        |          |
| EXECUTE  |        |    |        | ○        |
| INDEX    | ○      |    |        |          |
| INSERT   | ○      | ○  |        |          |
| SELECT   | ○      | ○  | ○      |          |

**객체권한 부여 문법**

위의 표에서 맨 왼쪽에 있는 ALTER, DELETE, EXECUTE.. 등은 object-privileges란에 오면 되고, 맨 윗줄에 있는 테이블, 뷰, 시퀸스, 프로시저 등은 ON 다음에 있는 Object에 입력하면 된다.

![객체권한 부여 문법](http://www.gurubee.net/imgs/oracle/sql/O_Privilege.jpg)

-	object_privilege : 부여할 객체권한의 이름
-	object : 객체명
-	user, role : 부여할 사용자 이름과 다른 데이터 베이스 역할 이름
-	PUBLIC : 객체권한, 또는 데이터베이스 역할을 모든 사용자에게 부여할 수 있다.
-	WITH GRANT OPTION : 권한을 부여 받은 사용자도 부여 받은 권한을 다른 사용자 또는 역할로 부여할 수 있게 된다.

**객체권한 부여 예제**

```SQL
-- scott USER에게 emp테이블을 SELECT, INSERT할 수 있는 권한을 부여했다.
-- scott USER도 다른 USER에게 그 권한을 부여 할 수 있다.
GRANT SELECT, INSERT
ON emp
TO scott
WITH GRANT OPTION;
 권한이 부여되었습니다.
```

**객체권한의 회수**

![객체권한의 회수](http://www.gurubee.net/imgs/oracle/sql/O_Revoke.jpg)

-	객체 권한의 철회는 그 권한을 부여한 부여자만이 수행할 수 있다.
-	CASCADE CONSTRAINS : 이 명령어의 사용으로 참조 객체 권한에서 사용 된 참조 무결성 제한을 같이 삭제 할 수 있다.
-	WITH GRANT OPTION 으로 객체 권한을 부여한 사용자의 객체 권한을 철회하면, 권한을 부여받은 사용자가 부여한 객체 권한 또한 같이 철회되는 **종속철회** 가 발생한다.

**객체권한 회수 예제**

```SQL
-- scott USER에게 부여한 emp 테이블에 대한 SELECT, INSERT 권한 회수 예제
-- 만약 scott USER가 다른 사용자에게 SELECT, INSERT권한을 부여했으면 그 권한들도 같이 회수가 된다.
REVOKE SELECT, INSERT
ON emp
FROM scott;
 권한이 회수되었습니다.
```

**WITH GRANT OPTION을 사용하여 객체권한 회수**

WITH GRANT OPTION을 사용하여 부여한 객체 권한을 취소하면 취소 작업이 연쇄적으로 수행 된다.

시나리오 1. SCOTT가 STORM에게 WITH GRANT OPTION을 사용하여 emp 테이블의 SELECT 권한을 부여 한다. 2. STORM이 emp 테이블의 SELECT 권한을 TEST에게 부여 한다. 3. SCOTT가 STORM에게 부여한 emp 테이블의 SELECT 권한을 취소 한다.

![시나리오](http://www.gurubee.net/imgs/oracle/sql/WithGrantOption.jpg)

결과 - SCOTT가 STORM에게 부여한 emp 테이블에 대한 SELECT 권한을 취소하면, TEST USER가 emp 테이블을 SELECT할 수 있는 권한도 자동으로 취소가 된다.

![결과](http://www.gurubee.net/imgs/oracle/sql/WithGrantOption2.jpg)

**객체권한관련 데이터 사전**

| 데이터 사전         | 설 명                                                                   |
|:--------------------|:------------------------------------------------------------------------|
| USER_TAB_PRIVS      | 객체권한의 소유자, 객체권한 부여자, 객체권한 피부여자를 볼수 있음       |
| USER_TAB_PRIVS_MADE | 사용자가 부여한 모든 객체권한                                           |
| USER_TAB_PRIVS_RECD | 사용자가 부여받은 모든 객체권한                                         |
| USER_COL_PRIVS      | 객체권한의 소유자, 객체권한 부여자, 객체권한 피부여자의 컬럼의 객체권한 |
| USER_COL_PRIVS_MADE | 사용자가 부여한 객체 컬럼에 대한 모든 객체권한                          |
| USER_COL_PRIVS_RECD | 사용자가 부여받은 객체 컬럼에 대한 모든 객체권한                        |

<br/>

##### 2.3.3. 롤(Role)

롤(ROLE) 이란 사용자에게 허가 할 수 있는 권한들의 집합 이라고 할 수 있다.

**롤(ROLE) 이란**

-	ROLE을 이용하면 권한 부여와 회수를 쉽게 할 수 있다.
-	ROLE은 CREATE ROLE 권한을 가진 USER에 의해서 생성 된다.
-	한 사용자가 여러개의 ROLE을 ACCESS 할 수 있고, 여러 사용자에게 같은 ROLE을 부여할 수 있다.
-	시스템 권한을 부여하고, 취소할 때와 동일한 명령을 사용하여 사용자에게 부여하고, 취소한다.
-	사용자는 ROLE에 ROLE을 부여할 수 있다.
-	오라클 데이터베이스를 설치하면 기본적으로 CONNECT, RESOURCE, DBA ROLE이 제공 된다.

아래의 그림처럼 DBA가 유저들에게 권한을 부여할 때 일일이 권한 하나하나씩을 지정을 한다면 몹시 불편할 것이다. DBA가 USER의 역할에 맞도록 ROLE을 생성하여서 ROLE만 유저에게 지정을 한다면 보다 효율적으로 유저들의 권한을 관리 할 수 있다.

| ROLE을 사용하지 않고 권한부여                                                       | ROLE을 사용하여 권한부여                                                       |
|:------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------|
| ![ROLE을 사용하지 않고 권한부여](http://www.gurubee.net/imgs/oracle/sql/roll_1.jpg) | ![ROLE을 사용하여 권한부여](http://www.gurubee.net/imgs/oracle/sql/roll_2.jpg) |

**ROLE 생성 문법**

![ROLE 생성 문법](http://www.gurubee.net/imgs/oracle/sql/roll_3.jpg)

**ROLE 부여 예제**

ROLE의 부여 순서 1. ROLE의 생성 : CREATE ROLE manager 2. ROLE의 권한 부여 : GRANT create session, create table TO manager 3. ROLE을 사용자 또는 ROLE에게 부여 : GRANT manager TO scott, test

```SQL
-- ROLE을 생성 합니다.
CREATE ROLE manager;
-- ROLE에 권한을 부여 합니다.
GRANT create session, create table TO manager;

-- 권한이 부여된ROLE을 USER나 ROLE에 부여 합니다.
GRANT manager TO scott, test;
```

**ROLE 관련 데이터 사전**

| 데이터 사전         | 설 명                                           |
|:--------------------|:------------------------------------------------|
| ROLE_SYS_PRIVS      | ROLE에 부여된 시스템 권한                       |
| ROLE_TAB_PRIVS      | ROLE에 부여된 테이블 권한                       |
| USER_ROLE_PRIVS     | 현재 사용자가 ACCESS할 수 있는 ROLE             |
| USER_TAB_PRIVS_MADE | 현재 사용자의 객체에 부여한 객체 권한           |
| USER_TAB_PRIVS_RECD | 현재 사용자의 객체에 부여된 객체 권한           |
| USER_COL_PRIVS_MADE | 현재 사용자 객체의 특정 컬럼에 부여한 객체 권한 |
| USER_COL_PRIVS_RECD | 현재 사용자 객체의 특정 컬럼에 부여된 객체 권한 |

<br/>

##### 2.3.4. 오라클 데이터베이스를 설치하면 기본적으로 생성되는 Role

오라클 데이터베이스를 생성하면 기본적으로 몇 가지의 ROLE이 생성 된다. DBA_ROLES 데이터 사전을 통하여 미리 정의된 ROLE을 조회 할 수 있다.

```SQL
SELECT * FROM DBA_ROLES;

ROLE                      PASSWORD
----------------------    -----------
CONNECT                   NO
RESOURCE                  NO
DBA                       NO
SELECT_CATALOG_ROLE       NO
EXECUTE_CATALOG_ROLE      NO
DELETE_CATALOG_ROLE       NO
EXP_FULL_DATABASE         NO
IMP_FULL_DATABASE         NO
....

이 외에도 많이 ROLE이 존재하는데, 가장 많이 사용하는 세 가지만 설명 하겠다.
```

**CONNECT ROLE**

-	오라클에 접속 할 수 있는 세션 생성 및 테이블 생성하거나 조회 할 수 있는 가장 일반적인 권한들로 이루어져 있다.
-	CONNECT ROLE이 없으면 유저를 생성하고서도 Oracle에 접속 할 수가 없다.
-	아래의 명령어로 CONNECT ROLE이 어떤 권한으로 이루어져 있는지 확인 할 수 있다.

```SQL
SQL>SELECT grantee, privilege
    FROM DBA_SYS_PRIVS
    WHERE grantee = 'CONNECT';

GRANTEE     PRIVILEGE
----------- ---------------------
CONNECT     ALTER SESSION
CONNECT     CREATE CLUSTER
CONNECT     CREATE DATABASE LINK
CONNECT     CREATE SEQUENCE
CONNECT     CREATE SESSION
...
```

RESORCE ROLE

-	Store Procedure나 Trigger와 같은 PL/SQL을 사용할 수 있는 권한 들로 이루어져 있다.
-	PL/SQL을 사용하려면 RESOURCE ROLE을 부여해야 한다.
-	유저를 생성하면 일반적으로 CONNECT, RESOURCE롤을 부여한다.

**DBA ROLE**

-	모든 시스템 권한이 부여된 ROLE이다.
-	DBA ROLE은 데이터베이스 관리자에게만 부여해야 한다.

### 3. 테이블의 생성과 수정 그리고 삭제

#### 3.1. 테이블의 생성

#### 3.2. 테이블의 제약조건

#### 3.3. 오라클 데이터 타입

#### 3.4. LOB, LONG, LONG RAW 데이터 타입 간의 비교

#### 3.5. 테이블의 관리

### 4. 데이터 조작어(DML)

#### 4.1. 데이터의 삽입, 수정, 삭제

##### 4.1.1. MERGE 문의 이해 및 활용

#### 4.2. SELECT문 및 연산자

#### 4.3. 예명(Alias)

#### 4.4. 조인(Join)

##### 4.4.1. Equi Join, Non_Equi Join, Self Join

##### 4.4.2. Outer Join (LEFT, RIGHT, FULL OUTER JOIN)

##### 4.4.3. CROSS JOIN, INNER JOIN, NATURAL JOIN, USING, ON

#### 4.5. 트랜잭션(commit과 rollback)

#### 4.6. Commit과 Rollback 예제

### 5. 내장 함수(Sing-Row Functions)

#### 5.1. Numeric Functions (숫자형 함수)

#### 5.2. Character Functions (문자형 함수)

#### 5.3. Datetime Functions (날짜 함수)

#### 5.4. Conversion Functions (변환 함수)

#### 5.5. 기타 함수들

#### 5.6. DECODE와 CASE

#### 5.7. NVL, NVL2, NULLIF, COALESCE

### 6. 집계함수(Aggregate function)의 이해

#### 6.1. 집계함수(Aggregate function)란?

#### 6.2. GROUP BY와 HAVING절

### 7. 서브쿼리(Subquery)

#### 7.1. Subquery란?

#### 7.2. Single-Row Subquery

#### 7.3. Multiple-Row Subquery

#### 7.4. Multiple-Column Subquery

#### 7.5. Inline View (From절 Subquery)

#### 7.6. Scalar Subquery

#### 7.7. UNION [ALL], INTERSECT, MINUS 연산자

### 8. 데이터 사전 (Data Dictionary)

#### 8.1. 데이터 사전(Data Dictionary)이란?

#### 8.2. 데이터 사전(Data Dictionary) 정보조회

### 9. 오라클 객체

#### 9.1. 인덱스(Index)

#### 9.2. VIEW 테이블

#### 9.3. 시퀀스(Sequence)의 이해 및 활용

#### 9.4. SYNONYM(동의어)
