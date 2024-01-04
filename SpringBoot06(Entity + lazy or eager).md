- 관계(Relation)
  * 관계형 데이터베이스에서는 개체(Entity)간의관계로 데이터를 표현
  * 1:1, 1:N, N:1, N:N의 형식
  * 관계를 구성하는 핵심 : PK(Primary Key) and FK(foreign Key)
  * 관계를 어떻게 해석하는지가 설계의 관건
  * 원하는 데이터가 남도록 작성하는 것

- 회원과 게시글
  * 한명의 회원은 여러 게시글을 작성 1:N
  * 하나의 게시글은 한명의 회원에 의해 작성 1:1

- 데이터의 개수로 판단
  * 가상의 데이터를 만들어 보는 것
  * 가상의 테이블에 존재하는 데이터의 개수를 파악하면 관계를 어떻게 그려야 하는지 판단 가능

- PK로 관계를, FK로 연관관계를
  * 데이터베이스 설계를 PK를 기준으로 해석해서 작성
  * JPA의 연관관계는 DB설계의 FK를 이용해서 연관관계를 시작
  * FK를 가진 쪽에 참조가 있듯이 클래스 내에 참조를 선언

- 프로젝트 생성
  * spring boot : 2.7.15
  * group : org.zerock
  * artifact : board
  * type : gradle
  * lang : java 11
  * packaging : war
  * dependencies
    + spring boot devtools
    + lombok
    + spring web
    + thymeleaf
    + spring data jap
  
- 날짜 시간 처리
  * BaseEntity class 생성
  * BoardApplication 
    + @ EnableJpaAuditing
  
- Entity 클래스 작성
  * @ManyToOne
    + ERD를 기준으로 엔티티간의 연관관계를 지정

- Repository 인터페이스 작성
  * Member, Board, Reply에 대한 각각의 인터페이스

- 테스트 코드 작성
  * Entity 클래스의 세팅
    + @Entity, @Getter, @Builder, @AllArgsConstructor
    + @ NoArgsCOnstructor, @ToString
  * 회원
    + Intstream.rangeClosed
    + builder
    + save
  * 게시물
  * 댓글

- ManyToOne 과 Eager/Lazy
  * 테이블 간 연관 관계는 객체의 참조를 통해 이뤄 진다.
  * Fetch Type : 참조하는 객체들의 데이터를 가져오는 시점을 정하는 것 
    + Eager : 즉시 로딩 -> 데이터를 가져올 때 하나의 객체만 가져오는 것이 아닌 참조 객체들의 데이터까지 전부 읽어오는 방식
    + Lazy  : 지연 로딩 -> 참조 객체 데이터들은 무시하고 해당 엔티티의 데이터만 가져오는 방식
  * 보편적으로 Lazy 지연로딩을 사용
    + 불필요한 조인으로 성능 저하를 막기 위해
  * Default setting
    + oneToMany > lazy
    + manyToMany > lazy
    + manyToOne > eager -> lazy 로 직접 변경
    + oneToOne > eager ->  lazy 로 직접 변경

- 지연(lazy)로딩의 이해
  * 필요하지 않는 데이터는 가능하면 로딩을 미루는 방식이 지연로딩
  * board.getWriter()를 실행하는 순간에 회원 정보가 추가적으로 필요
  * @Transactional을 적용하면 필요한 순간 다시 데이터베이스 연결

- 주의해야 하는 toString()
  * toString()시에 연관된 엔티티를 출력하는 경우에 다시 연결이 필요한 경우가 발생
  * 연관관계를 지정하는 경우에는 항상 toString()에서 제외

- JPQL의 left join
  * 부트 2.0부터는 엔티티 클래스 내에 참조가 없어도 left joni처리가 가능
  * 클래스 내부에 참조가 있는 경우
