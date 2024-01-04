   - 조인
    * 가로 연결 
    * from 절에 여러 테이블 지정
    * where 절을 활용한 조인 조건 사용의 중요성
    * 테이블의 별칭 설정
  - 조인 종류
    * 등가조인 : '=' 사용
    * 비등가 조인 : 등가 조인 외
    * 자체 조인 : 하나의 테이블을 여러 테이블처럼 사용
    * 외부 조인 : 조인 조건의 NULL 데이터도 출력
  - 표준 조인 문법
    * NATURAL JOIN : 두 테이블의 같은 열 기준
    * JOIN ~ USING : 조인에 사용할 기준열 명시
    * JOIN ~ ON : 조인 조건 직접 명시
    * OUTER JOIN : 외부 조인
5. 서브쿼리
  - 서브쿼리
    * 단일행 서브쿼리
      - 실행 결과가 단 하나의 행으로 나오는 서브쿼리
      - 단일행 연산자 사용
        * >, >=, = <=, <, <>, ^= !=
    * 다중행 서브쿼리
      - 실행 결과가 여러 개의 행으로 나오는 서브 쿼리
      - 다중행 연산자 사용
        * in, any, some, all, xists
      
----------------------------------------------------------------
* Join 
   - 두개 이상의 테이블에서 컬럼을 가져와서 하나의 테이블형태로 출력
   - RDB의 특성상 중요
* 등가 조인 = equi join
* 비등가 조인 = non equi join
* 자체 조인 = sef join
* 외부 조인 = outer join <-> inner join
* a=[1, 2, 3] b = [3, 4, 5];
  - inner = 3
  - left outjoin = 1,2,3
  - right outer join = 3, 4, 5
  - full outer join = 1, 2, 3, 4, 5
* a = [1,2, 3], b[4, 5];
  - inner = 4, 5
  - left outer join = 1,2,3
  - right outer join = 1,2,3,4,5
  - full outer join = 1,2,3,4,5
* ansi sql 
  - 표준 sql
  - 대부분의 RDB에서 실행되는 표준 SQL
* natural join
  - join 조건을 명시하지 않는 조인
  - join  조건으로 사용할 컬럼이 존재 하면 inner join처럼 동작
  - join 조건으로 사용할 컬럼이 존재하지 않으며 행의수 * 행의 수 만큼 출력됨 -> 안씀
* full outer join
  - ansi sql 로만 구현
* inner join
  - 대부분의 조인이 구현됨 defualt

* outer join
  - 한쪽 테이블의 목록이 다 나온 상태에서 다른 테이블 컬럼 출력할 때 사용
  - 목록이 다 나와야 할 때
* self join
  - 상위 상품 category 구할 때 
  - manager이름 구할때 (scott)
* Query Optimizer(쿼리 최적화기)
  - 쿼리를 분석해서 실행하기에 최적화된 방법(쿼리)을 찾아서 실행
  - 개발자가 잘못 작성한 쿼리도 더 나은 방법을 찾음
  - execute plan을 정해 줌 
  - f10을 눌러서 execute plan 확인 가능

* 일반적으로 subquery 보다 join을 사용하도록 권장

* 와이어 프레임
  - 개념 설계
* 프로토 타입
  - 상세 설계

-----------------------------
