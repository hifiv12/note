## Part 4

### REST방식으로 전환

  - 웹서비스
    * 과거
      + 고정된 브라우저의 주소창
      + 특정한 확장자를 이용하는 모델 2 .do
      + 특정한 파라미터에 의한 분기 구조
    * 현재
      + URI + 식별데이터
      + GET/POST/PUT/DELETE 다양한 전송 방식
      + 서버에서는 순수한 데이터만을 서비스
  
  - REST 방식
    * Representational State Transfer
    * URI는 하나의 고유한 리소스를 대표하도록 설계 + 전송방식을 결합해서 작업지정
    * 어노테이션 
      + @RestController : Rest방식 처리
      + @ResponseBody : 데이터 자체를 전달
      + @PathVariable : URI 파라미터 추출
      + @CrossOrigin : ajax의 크로스 도메인 문제를 해결해주는 어노테이션
      + @RequestBody : json데이터를 dto로 바인딩 처리

  - @RestController
    * 메서드의 리턴 타입으로 사용자가 정의한 클래스 타입을 사용할 수 있다.
    * JSON, XML로 자동으로 처리

  - 예제프로젝트의 준비
    * 데이터의 처리는 xml or json
    * jackson-databind, jackson-dataformat-xml, gson 라이브러리 

  - @RestController의 반환 타입
    * String
    * int
    * 사용자 정의 타입
    * ResponseEntity < 일반적
  
  - SampleVO, SampleController 작성

  - JSON/XML 테스트
    * @GetMapping 
    * localhost:8081/sample/get_sample

  - Collection타입의 객체 반환
    * List
    * Map 
      - 요상하게 map.put을 하면 json의 depth를 쉽게 줄 수 있을꺼 같은 느낌적인 느낌
      
  - ResponseEntity 타입
    * 단순히 데이터뿐만 아니라 브라우저의 HTTP상태 코드등 추가적인 데이터를 전달할 수 있다는 장점

  - @RestController의 파라미터
    * @PathVariable
      + 일반, rest 컨트롤러 사용 가능
      + URI 경로의 파라미터를 사용할 때
    * @RequestBody
      + JSON 데이터를 원하는 타입의 객체로 바인딩 하는 경우
    * form 태그
  
  - @PathVariable
    * URI 경로 중간에 들어간 값을 얻기 위해 사용
  
  - @RequestBody
    * 전송된 데이터가 JSON, 컨트롤러에서 사용자 정의 타입(DTO) 객체로 변환
    * lombok 사용

  - REST 방식의 테스트  
    * JUnit 기반의 테스트
    * 별도의 프로그램, 크롬 확장 프로그램(Talend API)

  - 다양한 전송방식과 URI 설계
    * create post
    * read get
    * update put
    * delete delete

  - 댓글 처리를 위한 테이블 설계

    ```sql
    create table tbl_reply (
      rno number(10,0), 
      bno number(10,0) not null,
      reply varchar2(1000) not null,
      replyer varchar2(50) not null, 
      replyDate date default sysdate, 
      updateDate date default sysdate
    );

    create sequence seq_reply;

    alter table tbl_reply add constraint pk_reply primary key (rno);

    alter table tbl_reply  add constraint fk_reply_board  
    foreign key (bno)  references  tbl_board (bno); 

    ```

  - ReplyVO 클래스 추가 / Mapper 준비
    * DTO, mapper, mapper.xml 하나의 셋트

  - Mapper CRUD 작업 
    * 외래키가 걸려 있으니 실제 존재하는 게시물 번호를 이용해서 테스트를 진행
    * mapper and mapper.xml 동시 작업

  - @Param 어노테이션과 댓글 목록
    + MyBatis의 파라미터는 1개만 허용
    + 해결하기 위해 
      - map, 클래스 , @Param 이용

  - 서비스영역과 컨트롤러 처리
    * ReplyService, ReplyServiceImpl 생성 및 작성
      + ReplyService
        - insert
        - read
        - delete
        - update
        - getListWithPaging
        - getcountByBno

  - ReplyController의 설계 
    * RequestMapping /replies
      + register : /new  POST
      + get : /:rno GET
      + delete : /:rno DELETE
      + modify : /:rno PUT or PATCH
      + page : /pages/:bno/:page GET

  - 등록작업과 테스트
    * 댓글 등록 > JSON으로 전달 > @RequestBody를 이용해 DTO 바인딩 > 처리결과 String 리턴

  - 특정 게시물의 댓글 목록
    * /pages/{bno}/{page}
    * consumes(들어올때 타입), produces(내려질 때 타입)
    * Criteria cri 는 echo로 그대로 전달할 목적으로 받는듯
    * 다만 현재 코드가 덜 완성된 상태라 json의 구조는 미약하게 다르게 감싸져있다.
  
  - 댓글의 삭제/조회
    * 조회는 특정 댓글만 내려주는 것 GET요청
    * 삭제는 특정 댓글의 번호를 통해 삭제 DELETE 요청

  - 댓글의 수정

  - ajax를 이용한 댓글 등록
    * src > main > webapp > js > reply.js 작성
    * get.jsp 에 script src 세팅 후 payload되는지 테스트
      + payload > 크롬 개발자모드 > network > 새로고침 > new > payload

  - 이후 댓글 CRUD 테스트

  - 댓글 페이지 
    * 이벤트 처리 및 HTML 처리
      + get.jsp html 코드 추가 
    * 댓글 목록 처리
      + $(document).ready(function() {});
        - functin showList(page)
    * 새로운 댓글의 처리
      + 모달창을 이용
      + 추가 후 처리
    * 특정 댓글 클릭 이벤트 
      + ajax로 가져온 결과를 dom 에 추가하는 형태의 댓글
      + 이벤트 위임(delegation) 방식을 이용해 처리
      + get.jsp
        - showList
        - modalCloseBtn
        - addReplyBtn
        - modalRegisterBtn
        - chat.onclick
          * modalModBtn
          * modalRemoveBtn
      + reply.js
        - add
        - getList
        - remove
        - update
        - get
        - displayTime
    
  - 댓글 페이징 처리
    * 데이터베이스의 인덱스 설계 
      + 모든 댓글은 게시물 번호를 기준으로 처리 > 게시물 번호의 정렬된 구조가 필요
    ```sql
      select /*+INDEX(tbl_reply idx_reply) */ 
      rownum rn, bno, rno, reply, replyer, replyDate, updatedate
      from tbl_reply
      where bno = 3145745(게시물 번호)
      and rno > 0;
    ```

