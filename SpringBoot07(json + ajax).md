  - 목록 화면에 필요한 JPQL
    * Board를 기준, Member와 Reply를 JPQL fh cjfl
  - 조회 화면에서 필요한 JPQL
    * 게시글 + 댓글 개수 + 회원
    * 댓글으 ㅣ데이터들은 Ajax를 이용해서 처리하는 것이 일반적

## 프로젝트 적용하기 
  - 게시물 등록 
    * DTO계층과 서비스 계층 작성
    * 테스트시 현재 데이터베이스에 저장되어 있는 이메일로 진행
  - 게시물 목록 
    * 파라미터 처리와 페이징 처리된 결과를 위한 PageRequestDTO와 PageResultDTO 추가
    * Object[]을 DTO로 변환

  - 게시물 조회

  - 게시물 삭제
    * 게시물이 삭제되면 댓글 데이터가 FK로 참조할 수 없으므로 주의
    * FK쪽을 우선 삭제 후 PK쪽을 삭제 -> 트랜잭션으로 처리 
  
  - 게시물 수정


  - 컨트롤러와 화면 처리
  - 목록 컨트롤로와 화면 처리

  - 게시물 등록 처리 및 화면처리
    * member 테이블에 존재하는 이메일을 작성해야됨

  - 게시물 조회 처리

  - 게시물 수정 / 삭제

  - JPQL을 이용할 때의 검색
  - 단일 엔티티가 아니므로 Querydsl에서 필요한 쿼리를 직접 동적으로 실행할 수 있는 구조가 필요
  - Repository를 확장해서 JPQLQuery 객체를 이용해서 직접 JPQL구문을 생성해서 처리

  - Repository를 확장하는법
    * 쿼리 메서드나 @Query등으로 처리할 수 없는 기능은 ㅕㅂㄹ도의 인터페이스로 설계
  - JPQLQuery 객체
    * 별도의 인터페이스에 대한 구현 클래스 작성, QuerydslRepositorySupport라는 클래스를 부모클래스로 사용
    * 구현 클래스에 인터페이스의 기능을 Q도메인 클래스와 JPQLQuery를 이용해서 구현
  - Tuple 객체

  - JPQLquery로 Page<오브젝트배열> 처리

  - Sort / count 처리

  - 목록 화면에서 검색 처리

## part 3-2
  - JSON 과 Ajax를 이용하는 댓글 처리
    * 화면에서 댓글 숫자를 클릭하면 댓글을 가져와서 출력
    * 새로운 댓글을 모달 창으로 통해서 등록
    * 댓글 수정과삭제 역시 특정 댓글 선택시 모달 창을 이용해서 처리

  - ReplyRepository 수정
    * 특정 게시물 번호에 해당하는 댓글을 가져오기

    ```java
      List<Reply> getRepliresByBoardOrderByRno(Board board);
    ```
    * ReplyRepositoryTests 테스트
  
  - ReplyDTO와 서비스 계층 처리
    * Reply 엔티티 객체를 DTO로 처리 하기 위한 클래스
    * ReplyService / ReplyServiceImpl 클래스
    * ReplyDTO 클래스 중 Board에 대한 참조 대신 bno 번호 

  - ReplyService의 기능
    * 기능 관련
      + dtoToEntity(ReplyDTO dto)
      + entityToDTO(Reply)
    * DTO와 엔티티 관련
      + register
      + getList
      + modify
      + remove

  - @RestController
    * Rest방식을 처리할 때 조금 더 수월하게 하는 용도일 뿐
    * @Responsebody 이 적용되는 형태
    * 주로 JSON이나 XML방식으로 리턴
    * ResponseEntity<> 타입이 권장
      + 데이터 + 상태 코드까지 같이 전송되는 것이 장점

  - 게시물의 댓글 목록 가져오기
    * 반환 타입의 제네릭 타입이 List<>
      + 목록과, 상태코드를 배열로 저장한 후 내릴려고 그런듯?

  - 화면에서 처리
    * read.html 수정 > list 버튼 이후 수정
    * 이후 모든 작업은 read.html 내 script 작업 과 컨트롤러만 
  


----------------------------------

소스코드(프로젝트) 고도화
-> 일반적으로 구현이 완료된 후 하는 작업
--> 성능개선(튜닝) - 개발자 입장 S/W에 한정
---> 로직 개선
---> 라이브러리 교체 ex> tomcat dbcp -> hikaricp, servlet upload -> 상용 upload library로 교체
---> 메모리 절약 session attribute 최소화, final static 상수 활용, String -> StringBuffer or StringBuilder 등으로 변경

--> 생산성향상 
---> 생산성이 정말 향상된거지 측정이 애매
---> 초기에 생산성이 향상된것 같아도 전체적으로 볼 때 오히려 더 생산성이 낮아지는 경우 있음
---> 개발+유지보수기간까지 종합적인 측정이 필요
      TOC(Total Of Cost) :S/W를 개발단계부터 배포 유지보수 폐기까지의 모든 비용

--> 트렌드에 맞춰서 변경
--> 눈치보여서
