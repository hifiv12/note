  - union
    * 테이블 끼리 같은 컬럼을 중복을 제거 해서 출력
    * 만약 중복을 허용할려면 union all
  - minus
    * a 와 b 의 테이블에서 a - b 하는 차집합
    * b에서 빼고난 a의 컬럼만 출력
  - intersect
    * 중복되는 컬럼만 출력

3. 오라클 함수
  - 함수
    * 내장 함수(built-in function) 
    * 사용자 정의 함수(user-defined function)
  - 내장 함수의 종류
    * 단일행 함수
    * 다중행 함수
  - 문자 함수
    * UPPER, LOWER, INITCAP -> 첫글자 대문자
    * LENGTH : 문자열 길이
    * SUBSTR : 문자열 일부 추출
      - substr(name, 2, 2) -> name은 컬럼, 2는 위치, 2는 가지고 올 개수
    * INSTR : 문자열 데이터 내 특정 문자 위치 찾기
    * REPLACE : 특정 문자를 다른 문자로 대체
    * LPAD, RPAD : 데이터의 빈 공간 채우기
    * CONCAT : 두 문자열 데이터를 합치기
    * TRM, LTRIM, RTRIM : 특정 문자 지우기
    * ROUND : 반올림
    * TRUNC : 버림
    * CEIL : 지정된 숫자와 가장 가까운 큰 정수
    * FLOOR : 지정된 숫자와 가장 가까운 작은 정수
    * MOD : 숫자를 나눈 나머지
  - DATE 데이터의 연산
    * SYSDATE : 현재 날짜와 시간
    * ADD_MONTHS : 몇 개월 이후 날짜
    * MONTHS_BETWEEN : 두 날짜 간의 개월수 차이
    * NEXT_DAY : 돌아오는 요일
    * LAST_DAY : 달의 마지막 날짜
    * ROUND, TRUNC : 날짜 반올림, 버림
  - 자료형을 반환하는 형 변환 함수
    * TO_CHAR : 숫자 또는 날짜 데이터를 문자 데이터
    * TO_NUMBER : 문자 데이터를 숫자 데이터
    * TO_DATE : 문자 데이터를 날짜 데이터
  - NULL 처리 함수
    * nvl : null이 아니라면 그대로 null이면 지정한 값
    * nvl2 : 각각 지정한 값
  - DECODE함수와  CASE문
    * 조건에 따라 다른 데이터를 반환 
    * DECODE
      - 기준 데이터를 지정
      - 기준 데이터에 따라 반환할 데이터 지정
    * CASE
      - 기준 데이터를 지정하는 방식
      - 기준 데이터를 지정하지 않는 방식

4. 다중행 함수와 데이터 그룹화
  - 다중행 함수
    * SUM
    * COUNT
    * MAX
    * MIN 
    * AVG
  - GROUP BY
    * 결과 값을 원하는 열로 묶어 출력
    * 기본 사용법
      - 그룹화할 열을 지정(여러 개 지정 가능)
    * 유의점
  - HAVING 
    * differ WHERE
  - 그룹화와 관련된 함수
    * ROLLUP, CUBE
    * GROUPING, SETS
    * GROUPING: ROLLUP OR CUBE
    * GROUPING_ID: ROLLUP, CUBE
    * LISTAGG:그룹 데이터 가로 출력
    * PIVOT, UNPIVOT : 행/열 바꾸어 출력

 ----------------------------------------------   
 sql 함수
  집계함수
  : sum, avg, min, amx, count
  : 공통
  그외의 함수들은 DB마다 다를 수 있다.
  
java에서 문자열을 다루는 함수와 비슷한 함수보다는
java에는 없는 함수, sql 함수로 하면 더 편리해지는 경우 위주로 정리

avg()를 사용 할 때 
:null 값을 0으로 취급할 것인지 확인필요
-> 비즈니스로직에 따라 다르다
-> nvl()사용해서 0으로 변경해서 사용여부를 판단

검색 조건이 복잡해지면서 sql로 처리하기가 점점 힘들어짐
-> OLAP, Data Mining등 기술이 도입됨
-> 빅데이터, no sql 기술로 발전