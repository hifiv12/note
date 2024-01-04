 - 빈 값을 허락하지 않는 not null
    * not null
      - 지정된 열에 null 저장불가
      - null 외 데이터의 중복은 허용
    * 제약 조건 확인
      - user_contraints
      - onwer : 소유 계정
      - constraint_name : 제약 조건 이름
      - constraint_type : 종류 C U P R
      - table_name : 지정한 테이블
    * 제약 조건 지정
      - 테이블을 생성하며 제약조건 지정
      - 제약 조건 이름 직접지정
      - 이미 생성한 테이블에 제약 조건 지정
    * 제약 조건 삭제
      - drop
  - 중복되지 않는 값 unique
    * unique
      - 지정된 열에 중복 데이터 저장 불가
      - null 저장은 가능
    * 제약 조건 확인 : user_constraints
    * 제약 조건 지정
      - 테이블을 생성하며 제약조건 지정
      - 제약 조건 이름 직접 지정
      - 이미 생성한 테이블에 제약 조건 지정
    * 제약 조건 삭제
      - drop
  - 유일하게 하나만 있는 값 primary key
    * primary key
      - 지정된 열에 중복 데이터 저장 불가
      - null 저장 불가
      - 자동으로 인덱스 생성
    * 제약 조건 지정
      - 테이블을 생성하며 제약 조건 지정하기
      - 테이블을 생성하며 제약 조건 이름 직접 지정하기
  - 다른 테이블과 관계를 맺는 foreign key
    * foreign key
      - 다른 테이블의primary key 참조
      - 참조하고 있는 키의 데이터와 null만 저장 가능
    * 제약 조건 지정
      - 테이블을 생성하며 제약 조건 지정하기
      - 테이블을 생성하며제약 조건 이름 직접 지정하기
    * foreign key로 참조 행 데이터 삭제하기
      - on delete cascade
      - on delete set null
  - 데이터 형태와 범위를 정하는 check
    * check
      - 열에 저장할 수 있는 값의 범위 또는 패턴을 정의
      - 조건식을 지정
  - 기본값을 정하는 default
    * default
      - 저장값이 없을 경우 기본 값을 지정
      
15. 사용자, 권한, 롤 관리
  - 사용자 관리
    * 사용자
      - 데이터 베이스에 접속하여 데이터를 사용/관리하는 계정
      - 업무의 분할과 효율, 보안을 고려하여 생성
    * 데이터베이스 스키마
      - 데이터를 저장 및 관리하기 위해 정의한 데이터 베이스 구조의 범위를 분류
    * 사용자 생성
      - create user > 사용자 이름(필수)
      - identified by > 패스워드(필수)
      - defualt tablespace > 테이블 스페이스 이름(선택)
      - temporary tablespace > 테이블 스페이스(그룹)이름(선택)
      - quota on > 테이블 스페이스 크기 on 테이블 스페이스 이름(선택)
      - profile 프로파일 이름(선택)
      - password expire (선택)
      - account [lock/unlock] (선택)
    * 사용자 정보 조회
      - ..._users
    * 오라클 사용자의 변경과 삭제
      - 변경 : alter
      - 삭제 : drop > cascade
  - 권한 관리
    * 권한
      - 접속 사용자에 따라 접근할 수 있는 데이터 영역을 지정
      - 시스템 권한, 객체 권한
    * 시스템 권한
      - 사용자 생성, 정보 수정, 삭제, 데이터 베이스 접근
      - 여러 자원과 객체 생성 미 관리 등의 권한을 포함
    * 시스템 권한 부여
      ```sql
        grant [시스템 권한] to [사용자 이름/롤(role)이름/public]
        [with admin option];
      ```
    * 시스템 권한 취소
      ```sql
        revoke [시스템 권한] from [사용자 이름/롤(role)이름/public]
      ```
    * 객체 권한
      - 특정 사용자가 생성한 객체와 관련된 권한
      - scott이 아닌 사용자가 scott 테이블에 insert
    * 객체 권한 부여
      ```sql
        grant [객체권한/all privileges]
        on [스키마.객체 이름]
        to [사용자 이름/롤(role)이름/public]
        [with grant option];
      ```
    * 객체 권한 취소
      ```sql
        revoke [객체권한/all privileges]--(필수)
        on [스키마.객체 이름]--(필수)
        to [사용자 이름/롤(role)이름/public]--(필수)
        [cascade constraints/force];--(선택)
      ```
  - 롤 관리
    * 롤
      - 여러 종류의 권한을 묶어 놓은 그룹
    * 사전 정의된 롤
      - connect
      - resource
      - DBA
    * 사용자 정의 롤
      - 필요에 의해 직접 권한을 포함시켜 생성한 롤

16. PL/SQL 기초
  - PL/SQL 구조
    * 블록
      - pl/sql 프로그램의 기본단위

      구성 키워드 | 필수/선택 | 설명
      -- | -- | --
      declare | 선택 | 실행에 사용될 변수, 상수, 커서 등을 선언
      begin | 필수 | 조건문, 반복문, select, dml, 함수 등을 정의
      exceoption | 선택 | ps/sql 실행 도중 발생하는 오류를 해결 문장 기술

      ```sql
        declare
          [실행에 필요한 여러 요소 선언];
        begin
          [작업을 위해 실제 실행하는 명령어];
        exception
          [pl/sql 수행 도중 발생하는 오류 처리];
        end;
      ```
    * 주석 
      - 실행되지 않는 문장
      - 한줄 주석 : '--'
      - 여러 줄 주석 : '/* */'
      - sql문에서도 사용 가능
  - 변수와 상수
    * 변수
      - 데이터를 일시적으로 저장
      - 저장되는 값의 변경 가능
      - 이름, 저장할 자료형을 지정
        ```txt
          변수이름 자료형 := 값 또는 값이 도출되는 여러 표현식
        ```
    * 상수
      - 한번 저장한 값이 프로그램 종료시까지 유지
      - constant 키워드 사용
        ```txt
          변수이름 constant 자료형 := 값 또는 값을 도출하는 여러 표현식;
        ```
    * 변수의 기본값 지정
        ```txt
          변수이름 constant 자료형 := 값 또는 값을 도출하는 여러 표현식;
        ```
    * 변수에 null값 저장 막기
        ```txt
          변수이름  자료형 not null :=  또는 default 값을 도출하는 여러 표현식;
        ```
    * 변수의 자료형
      - 스칼라형 : 내부 구성 요소가 없는 단일값
        
        분류 | 자료형 | 설명
        -- | -- | --
        숫자 | number | 소수점을 포함할 수 있는 최대 38자리 숫자 데이터
        문자열 | char | 최대 32,767바이트 고정 길이 문자열 데이터
        문자열 | varchar2 | 최대 32,767바이트 가변 길이 문자열 데이터
        날짜 | date | 기원전 4712년 1월 1일부터 서기 9999년 12월 31일까지 날짜데이터
        논리 데이터 | boolean | pl/sql에서만 사용할 수 있는 논리 자료형으로 true, false, null을 포함

      - 참조형 : 특정 테이블의 열, 행 구조를 참조
        * %type : 열참조
          ```txt
            변수이름 테이블이름.열이름%type
          ```
        * %rowtype : 행참조
          ```txt
            변수이름 테이블이름%rowtype
          ```
      - 복합형

        분류 | 자료형 | 설명
        -- | -- | --
        컬렉션 | table | 한 가지 자료형의 데이터를 여러 개 저장(테이블 열과 유사)
        레코드 | record | 여러 종류 자로형의 데이터를 저장(테이블 행과 유사)

      - LOB형
        * Large Object
  - 조건 제어문
    * if 조건문

      종류 | 설명
      if-then | 특정 조건을 만족하는 경우 작업 수행
      if-then-else | 특정 조건을 만족하는 경우와 반대 경우에 각각 지정한 작업 수행
      if-then-elsif | 여러 조건에 따라 각각 지정한 작업 수행
      - if-then
        ```txt
          if 조건식 then
            수행할 명령어;
          end if;
        ```
      - if-then-else
        ```txt
          if 조건식 then
            수행할 명령어;
          else 
            수행할 명령어
          end if;
        ```
      - if-then-elsif
        ```txt
          if 조건식 then
            수행할 명령어;
          elsif 조건식
            수행할 명령어;
          ...
          else
            수행할 명령어;
          end if;
        ```
    * case 조건문
      
      종류 | 설명
      -- | --
      단순 case문 | 비교 기준이 되는 조건의 값이 여러 가지일 때 해당 값만 명시하여 작업수행 
      검색 case문 | 특정한 비교 기준 없이 여러 조건식을 나열하여 조건식에 맞는 작업 수행

      - 단순 case

        ```txt
          case 비교 기준
            when 값1 then
              수행할 명령어;
            when 값2 then
              수행할 명령어;
            ...
            else
              수행할 명령어;
            end case;
        ```

      - 검색 case

        ```txt
          case 비교 기준
            when 조건식1 then
              수행할 명령어;
            when 조건식2 then
              수행할 명령어;
            ...
            else
              수행할 명령어;
            end case;
        ```

  - 반복 제어문
    * 반복문
      
      종류 | 설명
      -- | --
      기본 loop | 기본 반복문
      while loop | 특정 조건식 결과를 통해 반복 수행
      for loop | 반복 횟수를 정하여 반복 수행
      cusor for loop | 커서를 활용한 반복 수행

    * 반복 수행 제어
      
      종류 | 설명
      -- | --
      exit | 수행 중인 반복 종료
      exit-when | 반복 종료를 위한 조건식을 지정하고 만족하면 반복종료
      continue | 수행 중인 반복의 현재 주기를 건너뜀
      continue-when | 특정 조건식을 지정하고 조건식을 만족하면 현재 반복 주기를 건너뜀

    * 기본 loop
      ```txt
        loop
          반복 수행 작업
        end loop;
      ```
      - exit : 즉시 반복 종료
      - exitwhen : 종료 조건식 사용
    * while loop
      ```txt
        while 조건식 loop
          반복 수행 작업;
        end loop;     
      ```
    * for loop
      ```txt
        for i in 시작 값 .. 종료값 loop
          반복 수행 작업;
        end loop;     
      ```
    * continue
      - 즉시 다음 반복 주기로 이동
    * continue-when
      - 특정 조건식 만족 여부에 따라 다음 반복 주기로 이동
  
17. 레코드와 컬렉션
  - 자료형이 다른 여러 데이터를 저장하는 레코드
    * 레코드
      - 자료형이 다른 데이터를 하나의 변수에 저장

        ```sql
          type 레코드이름 is record(
            변수이름 자료형 not null := (또는 default) 값 또는 값이 도출되는 여러 표현식
          ) 
        ```

    * 레코드를 사용한 insert
    * 레코들르 사용한 update
    * 레코드를 포함하는 레코드
      - 중첩 레코드
  - 자료형이 같은 여러 데이터를 저장하는 컬렉션 
    * 컬렉션
      - 특정 자료형의 데이터를 여러 개 저장
        ```txt
          * 연관 배열 (associative array or index by table)
          * 중첩 테이블 (nested table)
          * VARRAY (variable-size array)
        ```
    * 연관 배열
      ```sql
        type 연관배열이름 is table of 자료형 [not null]
        index by 인덱스형;
      ```
    * 컬렉션 메서드
      - exist(n)
      - count
      - limit
      - first
      - last
      - prior(n)
      - next(n)
      - delete
      - extend
      - trim
------------------------------------------------------------------

Foreign key
  다른 테이블의 Primary key값이 아닌 다른 값이 저장되는 것을 막아준다.
  -> RDB는 테이블 간에 Relation을 맺어 저장하게 되는데 FK가 중요한 역할을 한다.
  -> FK가 없으면 데이터를 신뢰할 수 없게됨, 참조 무결성(Integrity)이 보장되지 않는다.

erd
  테이블간의 관계를 그린 그림
  -> PK, FK, 관계를 그린 그림

on delete cascade
  primary key 값이 삭제되면 foreign key값도 같이 삭제됨
on update cascade
  primary key 값이 변경되면 foreign key값도 같이 변경됨
  -> oracle은 지원하지 않음

check
   validation에 사용
  -> 일반적으로 web에서는 사용자 입력값의 validation을 javascript or jquery로 구현
  -> check는 사용빈도가 적으나, db차원의 validation이므로 더 확실함.

constraint 명을 작성하는게 좋을까?
  1 관리차원에서는 있는게 편리
  2 배포할 때 같은 이름의 contraint가 이미 존재하면 에러남
  -> 개발자가 작성한 코드에 포함될 때는 name이 없는것이 더 낫다.

schema(구조)
  data base나 table의 구조를 말함
  계정명을 schema명으로 사용
scott.emp
  scott은 계정명이면서 schema명

ora_user.emp
  ora_user가 만든 emp

권한과 role은 보안문제와도 연관됨
개발자, 사용자에 역할에 맞는 최소한의 권한을 부여하는 것이 좋다.
  결국 보안은 사람이 문제
    1. 내부 
    2. 외부
    모두 사람이 보안과 직결됨

back door
  개발자가 자신만 아는 접속방법이나 기능을 심어놓는 것

보안을 철저히 한다고 해도 문제가 발생할 여지가 늘있음
백업 철저

pl/sql
  oracle에서 사용하는 확장된 sql
  -> 변수, if문, 반복문, 함수, stored procdure, trigger