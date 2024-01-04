10.  데이터를 추가, 수정, 삭제하는
데이터 조작어

  - insert 
    * 테이블이 데이터를 추가하는 insert문
    * insert into table_name values(value, value...);
  - null
    * null 명시적 입력 - 입력부분에 입력
    * null 암시적 입력 - 입력해야될 부분을 공백
  - 테이블에 날짜 데이터 입력
    * 직접 입력
    * to_date 함수 사용
    * sysdate 함수 사용
  - 서브쿼리 사용 시 여러 데이터 추가
    * values 절 사용하지 않기
    * 테이블의 열 개수 = 서브쿼리 열 개수 일치
    * 테이블의 자료형 = 서브쿼리 자료형 일치
  - update문의 사용법
    * update table_name set column1=data, column2=data,... where 
    * where 절로 일부분만 수정
  - 서브쿼리 사용 시 데이터 수정
  - update문 사용 시 유의점
    * where절 검증
  - delete문의 형식
    * delete from table_name where 조건식
    * 조건식을 사용해 일부분만 삭제
    * 서브쿼리 사용 가능

11. 트랜잭션 제어와 세션
  - 하나의 단위로 데이터를 처리하는 트랜잭션
    * 트랜잭션
      - 더이상 분할할 수 없는 최소 수행 단위
      - 한 개 이상의 DML
      - all or nothing
  - 트랜잭션을 제어하는 명령어
    * TCL(Transaction Control Language)
      - 트랜잭션을 제어하기 위해 사용하는 명령어
      - ROLLBACK : 트랜잭션 취소
      - COMMIT : 트랜잭션 영원히 반영
  - 세션과 읽기 일관성의 의미
    * 세션이란
      - 데이터베이스 접속을 시간으로 접속을 종료하기까지 전체기간
      - 하나의 세션에는 여러 개의 트랜잭션이 존재
    * 읽기 일관성
      - 특정 세션에서 수행하는 데이터의 변경이 확정되기 전까지,
      다른 세션에서 본래의 데이터를 보여줌
      - sql developer 에서는 삭제이지만 sql plus에서는 보여짐
  - 수정 중인 데이터 접근을 막는 LOCK
    * 데이터 잠금
    * 조작중인 데이터를 다른 세션이 조작할수 없음
    * LOCK 종류
      - 행 레벨 록 : 조작중인 행에 lock
      - 테이블 레벨 록 : DML을 사용해 데이터가 변경중인 테이블에 lock,
      데이터 정의어(DDL) 사용불가

12. 데이터 정의어
  - 객체를 생성, 변경, 삭제하는 데이터 정의어
    * 데이터 정의어를 사용할 때 유의점
      - auto commit 데이터 정의어 명렁이 수행되면 rollback 불가
  - 테이블을 생성하는 create
    * create문
    * create user.table_name (column1_name column1_data_type, .... )
    * 기존 테이블 열 구조와 데이터를 복사하여 새 테이블 생성하기
      - select문 사용
    * 기존 테이블 열 구조와 일부 데이터만 복사하여 새 테이블 생성하기
      - select ~ where절 사용
    * 기존 테이블의 열 구조만 복사하여 새 테이블 생성하기
      - 조건식이 항상 false인 where절 사용
  - 테이블을 변경하는 alter
    * add : 테이블에 열추가
    * rename : 테이블의 열 이름 변경
    * modify : 테이블의 열 자료형을 변경
    * drop : 테이블의 특정 열을 삭제
  - 테이블 이름을 변경하는 rename
    * rename : 변경 후 본래의 테이블 이름 사용 불가
  - 테이블의 데이터를 삭제하는 truncate
    * truncate
      - where절을 사용하지 않는 delete문
      - 테이블의 전체 데이터를 삭제
      - DDL-> rollback 불가
  - 테이블을 삭제하는 drop
    * drop
      - 테이블과 저장된 데이터 모두 삭제

13. 객체 종류
  - 데이터베이스를 위한 데이터를 저장한 데이터 사전
    * 데이터 사전
      - 데이터베이스를 구성하고 운영하는데 필요한 저오
      - 데이터 사전 뷰
      - 접두어가 존재
    * user_ 접두어를 가진 데이터 사전 : 접속한 사용자가 소유한 객체 정보
    * all_ 접두어를 가진 데이터 사전 : 접속한 사용자가 소유하거나, 사용을 허가 받은 객체 정보
    * dba_ 접두어를 가진 데이터 사전 : 데이터베이스 관리 권한을 가진 사용자가 조회 가능
  - 더 빠른 검색을 위한 인덱스
    * 인덱스
      - 데이터 검색 성능 향상을 위해 테이블 열에 사용하는 객체
      - USER_INDEXES
      - UNSER_IND_COLUMNS
    * 인덱스 생성
      - create index index_name on table_name (column1 asc ordesc, ...)
    * 인덱스 삭제
      - drop
  - 테이처럼 사용하는 뷰
    * 뷰
      - select문을 저장한 객체
    * 목적
      - 편의성 : select문의 복잡도 완화
      - 보안성 : 테이블의 일부 데이터만 노출
    * 뷰의 생성
      - create (or replace) [force | noforce] view view_name(column1, ...) as (select문) width check option constraint 제약조건 with read only constraint 제약조건
      - replace : 수정할 때
    * USER_VIEW
    * 뷰 삭제 
    * 인라인 뷰를 사용한 TOP-N SQL문
  - 규칙에 따라 순번을 생성하는 시퀀스
    * 시퀀스
    * 시퀀스 생성
      - create sequence sequence_name
      - increment by n : 증가값
      - start with n : 시작값
      - maxvalue n | nomaxvalue : 최고값
      - minvalue n | nominvalue : 최저값
      - cycle | nocycle : 순환
      - cache n | nochace : 메모리에 적재
    * 시퀀스 사용
      - currval : 시퀀스 마지막 생성 번호
      - nextval : 다음 번호 생성
    * 시퀀스 수정 : alter
    * 시퀀스 삭제 : drop
  - 공식 별칭을 지정하는 동의어
    * 동의어
      - 객체 이름 대신 사용할 수 있는 다른 이름
    * 동의어 생성
      - create [public] SYNONYM 동의어 이름 for [사용자].[객체이름]
    * 동의어 삭제 : drop
  
14. 제약 조건
  - 제약 조건 종류
    * 제약 조건 : 테이블 열에 저장될 데이터의 특성, 조건을 지정
    * not null : 지정열에 null 불허용
    * unique : 유일값
    * primary key : 유일값이면 not null
    * foreignkey : 다른 테이블의 열을 참조(존재하는 값만)
    * check : 설정한 조건식을 만조하는 데이터만 입력
 
    
      
----------------------------------------------
create table ...select문 : select한 결과를 가지고 table을 생성
insert into ...select문 : select한 결과를 가지고  table에 입력

create - insert
read -  select
update - update
delete - delete

Session
-> user가 server에 접속된 상태 or 상태를 저장하는 객체

Session이 몇개야?
-> 접속자가 몇개야 or sesstion 객체가 몇개

update가 자주 발생하면
transaction 처리에 로드가 걸림
update 횟수를 줄여서 전체 시스템 지연을 줄이는 것도
튜닝할 때 고려사항 중 하나임

update가 발생하면 index도 수정해야함

create문을 사용하면 auto commit
: 아직 commit하지 않은 insert, update, delete도 commit
-> create문은 실행하기 전에 반드시 insert, update, delete 작업을
먼저 commit, rollback

index
  검사속도 향상을 위해 만드는 객체
  책의 index 와 원리가 비슷함
  sorting이 되어 있음
  데이터의 위치(row id)가 적혀 있음

row id 
  행을 식별할 수 있는 unique한 값
  ->insert되면 oracle이 row id를 자동 생성함

  ->primary key가 생성되면 index가 자동생성됨

  ->index도 데이터가 추가되는 것임
    -> 테이블의 데이터가 많을 수록 index크기도 커짐
    update를 하면 index도 수정됨
    테이블의 데이터가 아주 많은 경우에는 index를 구성하는 시간도 오래걸림

where절에 나오는 column을 index로 만드는 것이 기본
ex) select* from emp sal=5000; <- 검색 속도가 느리면
create index idx_emp_sal on emp(sal);
primarykey를 만들면 index가 자동생성 되게 한 이유 
  primarykey가 where절에 가장 많이 사용되는 column이라서   

DML
1.select
2.insert
3.update
4.delete    

DDL (Data Definition Language)
1.create - 생성 
2.alter - 수정
3.drop - 삭제

DCL
1.grant - 권한 부여
2.revoke - 권한 회수

TCL
1.commit
2.rollback

통계쿼리가 일반적으로 제일 어렵다
  실력을 기르려면 통계부분을 담당하세요
  지옥문 시작 실력향상

view 
  select한 결과로 만들어 지는 가상 테이블
  ->데이터를 저장하지 않는다.
  ->view를 사용할 때 잠깐 데이터가 생성되었다가 소멸됨
  ** view를 이용해ㅓㅅ 데이터를 저장하거나 index를 생성하는 옵션이 
  나중에 추가됨

view와 다른 테이블도 조인가능

sequence
  일련번호를 만들 때 사용
  중복이 되지 않게 자동으로 만들어짐
  중간 번호를 삭제했을때 번호가 다시 조정되지는 않음

  1, 2, 3, 4

select max(bno)+1 from 