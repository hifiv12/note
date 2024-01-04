## 관계형 데이터베이스와 오라클 데이터베이스
1. 구성요소 
  - 테이블 
    * 행
    * 열
    * 키 
      - PK : Primary Key - unique key
      - alternate Key - unique key의 보조키
      - FK : Foreign Key - 다른 테이블의 일반 키 or unique key
        - reference key - 다른 테이블의 unique key
        - 참조키 or 외래키 
          * 참조무결성 유지
          * 식별관계: 참조키가 기본키 역할도 하는 경우 
          * 비식별관계 : 참조키가 기본키 역할을 하지 않는 경우
            - 일반적으로 식별관계를 권장하지 않음

      - composite key - 다른 컬럼과 2개 이상 복합된 키
- ERD(Entity Relationship Diagram)

2. 오라클 데이터베이스
  - 오라클 데이터베이스와 버전
    * 실습은 11g 사용
  - 자료형
    * VARiable CHARacter : 가변길이 문자열
      - VARCHAR2(length)
      - 1 ~ 4000byte 문자열
      - 주소, 이름, 학과명 등 길이가 일정하지 않은 데이터에 적합
    * CHARacter: 고정길이 문자열
      - 길이가 일정한 데이터에 적합
      - 우편번호, 휴대전화 번호 , 주민등록번호
      - char(3)
      - 글자를 꽉 안채운다면 남은 자리만큼 공백으로 채워짐
    * NUMBER
      - +_ 자릿수 숫자 저장
      - NUMBER(p, s) : p -> 정수 / s -> 소수점 자리 지정
    * DATE
      - 세기, 연, 월, 일, 시, 분, 초 
  - 객체 
    * 테이블 : 저장소
    * 인덱스 : 검색 효율
    * 뷰 : 데이터를 논리적으로 연결하여 하나의 테이블화
    * 시퀀스 : 일련 번호 생성
    * 시노님 : 오라클 객체의 별칭을 지정
    * 프로시저 : 프로그래밍 연산 및 기능 수행이 가능 -> 반환 값 없음
    * 함수 : 프로그래밍 연산 및 기능 수행이 가능 -> 반환 값 있음
    * 패키지 : 프로시저와 함수를 보관
    * 트리거 : 데이터 관련 작업의 연결 및 방지 관련 기능을 제공
  - PL/SQL

  - 개발 과정 변천사 
    * Main frame
      - 거대한 규모가 큰 중앙집중방식 시스템
      - 완전한 중앙집중방식
      - 모든 연산과 저장을 홀로 담당
      - terminal은 입출력만 담당
    * Server & Client (CS)
      - 서버와 클라이언트가 분산 처리
      - pc가 보급되면서 Terminal이 PC로 대체
      - 클라이언트를 활용하자는 생각에서 시작
    * Web
      - Client, Web server, DB server
      - CS보다 유지보수에 편리
    * App
      - Client(App), DB server
      - Client(App), Web server, DB server

  - SQL 
    * select - 검색 조회 -> 글쓰기 -> create
    * insert - 입력 -> 글보기 -> read
    * update - 수정 -> 글수정 -> update
    * delete - 삭제 -> 글삭제 -> delete
  
  - select
  - from
  - distinct
  - all
  - as
  - order by
  - where
    * 조건
      - and, or
      - 산술 연산자
      - 비교 연산자 
      - 논리 부정 연산자
      - IN 연산자
      - between a and b 연산자

- 오늘의 프로세스
  * 오라클 설치
  * 디벨로퍼 설치
  * 디비 생성
  * 유저 생성
  * 유저에게 권한 설정
  * 생성된 유저계정으로 접속
  * 테이블 생성
  * 데이터입력
  * 조회, 수정, 삭제...