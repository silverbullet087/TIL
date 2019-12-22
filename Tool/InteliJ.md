InteliJ 맥 단축키
=================

-	개발하면서 알게된 단축키나 추가 메모 사항은 계속 추가 예정.
-	[해당 단축키 출처:DevOOOOOOOOP 블로그](http://redutan.github.io/2016/03/23/intellij-favorite-keymap-osx) 의 내용 중 내가 필요한 부분과 내가 알게되 내용 추가

목차
----

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

-	[맥 OS 버튼](#맥-os-버튼)
-	[파일](#파일)
-	[Layout](#layout)
-	[Refector](#refector)
-	[에디터](#에디터)
-	[실행](#실행)
-	[생성](#생성)
-	[이동](#이동)
-	[검색](#검색)
-	[바로가기](#바로가기)
-	[Syntax](#syntax)
-	[추가](#추가)

<!-- /code_chunk_output -->

### 맥 OS 버튼

-	⌘ : command
-	⌃ : control
-	⇧ : shift
-	⌥ : option(alt)
-	⎋ : esc
-	⏎ : return(enter)
-	⇥ : tab

### 파일

-	⌘O : 클래스 찾기 - 단어사이 대문자로 조회하면 더 이득
-	⌘⇧O : 파일 찾기 - 유사 단축키로 ⇧⇧ 도 많이 사용함
-	⌘E : 최근 사용 파일 찾기
-	⌃⇥ : 최근 파일로 이동 - 위 ⌘E 와 유사하나 UX가 약간 다름

### Layout

-	⌘1 : Project view
-	⌘4 : Run view

### Refector

-	⌘⌥M : 메서드 분리
-	⇧ F6 : rename

### 에디터

-	⌘⇧↑, ⌘⇧↓ : 선택된 코드 영역 위, 아래로 이동
-	⌘ Del : 한 줄 삭제
-	⌘⇧] : 에디터 탭 기준 오른쪽으로 이동
-	⌘⇧[ : 에디터 탭 기준 왼쪽으로 이동
-	⌥↑ : 커서 기준으로 단위 영역(단어, 영역, 문장, 메서드 등) 선택 - 강추
-	⌘ F12 : 현재 클래스 필드, 메서드 등 목록 노출 - lombok 사용할 시 편함
-	⌘N : 각종 코드 생성 (getter, setter, override, DI 등)
-	⌃O : 상위클래스 override
-	⌃⌥O : Auto import
-	⌥⇥ : 스플릿(화면분할) 상태에서 화면 간 이동
	-	Split Vertical 단축키를 지정하고 쓰면 더 좋음 - 저는 ⌃⌥V로 지정
-	⌥ F1 then 1 or ⏎ : 현재파일 Project View 에서 활성화

### 실행

-	⌃R : 최근 실행한 것을 다시 실행
-	⌃D : 최근 실행한 것을 다시 실행 - 디버깅 모드

### 생성

-	⌘⇧T : 테스트케이스생성
	-	이후 ⌘N 을 이용하면 테스트메서드 생성이 편리함

### 이동

-	⌘B : 클라이언트 코드에서 해당 메소드 선언으로 이동
-	⌘⌥B : 클라이언트 코드에서 해당 메소드 구현으로 이동 - 강추
-	⌘⌥←, ⌘⌥→ : 이전, 다음 작업영역으로 이동

### 검색

-	⌘⇧F : 문자열 전체 검색

### 바로가기

-	⌘, : 환경설정
-	⌘; : 프로젝트 환경설정

### Syntax

-	iter : for-each 구문 생성
-	fori : for 구문 생성
-	psfs : public static final String
-	psfi : public static final int
-	psvm : public static void main(String[] args)
-	thr : throw new

### 추가

-	메소드 작성 후 알트 + 엔터 로 해당 클래스에 메소드 자동 생성
-	소스에서 커멘드 + N 으로 getter, setter 등 자동완성
-	왼쪽 파일 트리에서 커맨드 + N 으로 클래승 파일 생성
