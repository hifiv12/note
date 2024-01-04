  - ex2
    * mariadb install and setting
    * start.spring.io

## Spring Data JPA
  - ORM and JPA
    * ORM(Object-Relational Mapping) : 객체 관계 매핑
      + 관계형 데이터베이스를 객체로 처리
      + SQL 대신 객체지향언어를 활용   
    * JPA(Java Persistence API)
      + ORM을 java를 사용해서 구현하기 위한 표준 스펙 
    * Hibernate
      + JPA기반의 구현체 중 하나, 오픈소스
    * Spring Data JPA
      + Hibernate 기반으로 spring개발자들이 만듦
      + 줄여서 JPA라고 하는 경향
      + sql로 변환되어 실행됨 -> 성능상 이점은 없음
      + 직접 nvative query를 사용할 때 불필요한 쿼리가 추가적으로 작성되서 동작함

  - Entity Class와 JpaRepository
    * @Entity : 해당 클래스가 entity class임을 표시, 한개 이상의 테이블 생성
    * @Table : 관계형 데이터베이스에 생성되는 테이블과 관련된 설정
    * @Id : PK 관련 설정
    * @GeneratedValue : 자동으로 생성되는 방식
  - ddl (data definition language)
    * 데이터 정의 언어 -> create, alter, drop

  - spring.jpa.hibernate.ddl-auto=update
    * 옵션, 사용하지 않을 경우 table이 자동 생성되지 않음
    * table이 존재하면 alter 구문 동작
    * 없다면 create 구문 동작
  - spring.jpa.hibernate.ddl-auto=create : 일반적으로 사용하지 않음

  - 쿼리 메서드 기능과 @Query 
    * spring data jpa 는 동적 쿼리가 지원되지 않음 -> querydsl을 사용해
    * 쿼리 메서드 = 메서드의 이름 자체가 질의문이 되는 기능
    * 쿼리 메서드의 리턴 타입
      + select를 이용하는 작업의 경우 List타입 또는 배열 가능
      + Pageable 타입을 지정하면 Page<> 타입
    * 쿼리 메서드와 Pageable의 결합
      + 페이지 처리와 order by처리 가능
      + 대부분의 경우 쿼리 메서드는 정렬조건은 만들지 않고, Pageable파라미터를 이용하는 경우가 많음
    * @Query 어노테이션
      + 쿼리 메서드보다 직관적으로 JPQL을 이용해서 작성
      + 좀 더 다양한 조건이나 필요한 칼럼들만 추출할 수 있는 장점
      + 필요한 경우에는 순수한 SQL을 그대로 사용 가능
      + 쿼리 메서드가 주로 select에 초점을 두는 반면 DML처리가 좀 더 수월
    * @Query의 파라미터 바인딩과 페이징 처리
      + 파라미터 순서를 이용해 바인딩
        - :param_name : 파라미터 이름 활용
        - :#{} : 자바 빈 스타일 이용방식
      + 페이징 처리
        - countQuery : 
        - Object[] 리턴
          * 필요한 칼럼들(엔티티 객체들의 속성들)만 지정해서 추출하는 기능
          * 주로 JPQL의 함수 사용시에 유용
            - JPQL(Java Persistence Query Language)
              * 내가 원하는 컬럼만 바꿀 수 있는게 장점
            - JPA에 포함된 쿼리 언어
            - Native SQL과 비슷하나 table, column이 아닌 entity class의 instance, field(perperty)를 사용한 쿼리 언어
          * Native SQL
            - nativeQuery 속성을 true로 지정하면 일반 SQL을 그대로 사용할 수 있음
            - 정말 복잡한 쿼리를 사용할 때


-------------

빌더 패턴
  생성자 오버로딩을 사용하지 않고 객체를 생성하기 위한 패턴
  Builder Class를 추가 생성해서 사용
  Builder Class안에 Setter는 일반적으로 필드명과 동일하게 작성
  Builder Class안에 
