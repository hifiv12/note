# PL/SQL
  - Oracle's Procedural Language extension to SQL
  - SQL문에서 변수정의, 조건처리, 반복처리등을 지원하는 procedure Language
  - 구조
    * DECLARE문을 이용하여 정의 (선택적 명시)
    * BEGIN문을 이용하여 실행 (필수 명시)
    * EXCEPTION문을 이용하여 에러정의 (선택적 명시)
    * END문을 이용하여 종료 (필수 명시)
  - 장점
    * BLOCK 구조로 다수의 SQL문을 한번에 ORACLE로 보내서 처리함 -> 속도가 빠르다.
    * 모듈화가 가능
    * VARIABLE, CONSTANT, CURSOR, EXCEPTION을 정의하여 SQL문과 procedure문에서 사용
    * 복잡한 데이터 형태의 변수도 선언 가능
    * 테이블의 데이터 구조와 컬럼명에 맞게 동적으로 변수 선언 가능
    * EXCEPTION문을 이용해 Oracle server Error를 처리
    * 사용자 정의 에러를 선언하고 EXCEPTION 처리 루틴으로 처리 가능

## PL/SQL Block Structure
  - 논리적인 블록으로 나누는 구조화된 블록 언어
  - 선언부와 예외처리부는 선택적으로 구성
  - 실행부는 필수적으로 구성하며 BEGIN과 END 키워드는 반드시 기술

1. Declarative Section
  - 변수, 상수, cursor, user_define Exception 선언

2. Executable Section
  - SQL, 반복문, 조건문 실행
  - 실행부는 BEGIN으로 시작, END로 종료
  - 필수로 사용

3. Exception Handling Section
  - 예외에 대한 처리
  - 일반적으로 오류를 정의, 처리
  - 선택사항

4. PL/SQL 프로그램의 작성 요령ㄴ
  - PL/SQL 블록내에 문장마다 종료시 세미콜론(;)을 사용
  - END; -> 하나의 블록이 끝났다는 것을 명시
  - -- -> 단일행 주석
  - /* */ -> 여러행 주석
  - / 가 있으면 블록 종결

## PL/SQL 블럭의 유형

1. Anonymous Block

2. Procedure

3. Function 