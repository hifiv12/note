  - REST 방식
    * @RestController : Rest방식을 처리하기 위함
    * @ResponseBody : 뷰가 아닌 데이터 자체를 전달하기 
    * PathVariable : URL 경로에 있는 값을 파라미터로 추출할 때 
    * CrossOrigin : Ajax의 크로스 도메인 문제를 해결 
    * RequsetBody : Json 데이터를 원하는 타입으로 바인딩 처리
  
  - @ResController
    * Spring 4
    * 해당 Controller의 모든 메서드의 리턴 타입을 기존과 다르게 처리
    * 사용자가 정의한 타입을 사용, return Json or XML
  
  - 예제 프로젝트의 준비
    * jackson-databind : 2.9.6
    * jackson-dataformat-xml : 2.9.6
    * gson : 2.8.2

  - @RestController의 반환타입
    * String or Integer
    * 사용자 정의 타입
    * ResponseEntity<> 타입 > 주로 일반적 사용
  
  - SampleVO, SampleController
    * SamplVO
      + @Data
      + @AllArgsContructor : ?
      + @NoArgsContructor : ?
    * SAmplController
      + @RestController
      + @REquestMapping("/sample")
      + @Log4j
      + @GetMapping()
        - MediaType? > XML 과 Json타입 요청에 따른 반환값 encoder 느낌
    * test
      + defualt
      + Collection 타입의 객체 반환 List
      + Collection 타입의 객체 반환 Map
      + ResponseEntity<> 타입

  - @RestController의 파라미터
    * @PathVariable
      + Rest 방식에서 자주 사용 > URL경로의 일부를 파라미터로 사용 할 때 
      + <form>방식으로 처리된 데이터
    * @RequestBody
      + 전송된 데이터가 JSON이고 이를 컨트롤러에서 사용자 정의 타입의 객체로 변환 할 때 사용
      + 일반적으로 browser에서는 json형태의 데이터를 전송불가 > 별도의  REST 도구를 이용해 테스트
    * Test Tool 
      + Talend Rest API : 크롬 확장 프로그램 추가

  - 다양한 전송방식과 URI 설계
    * REST 방식의 데이터 교환에서 가장 특이한 점은 기존의 GET/POST 외의 다양한 방식으로 데이터를 전달

    작업 | 전송방식 | URI
    -- | -- | --
    Create(등록) | POST | /members/new
    Read(조회) | GET | /members/{id}
    Update(수정) | PUT | /members/{id} + body (json 데이터등)
    Delete(삭제) | DELETE | /member/{id}

## ajax를 이용한 댓글처리
  - 댓글 처리를 위한 테이블 설계
  
  - ReplyVO 클래스 추가 및 Mapper 준비

  - Mapper CRUD 작업(create)
  
  - Mapper 특정 댓글 조회

  - Mapper 특정 댓글 삭제 / 수정

  - @Param 어노테이션과 댓글 목록
    * 파라미터를 2개 이상 받기
      + Map형태 사용
      + 별도 클래스 이용
      + @Param을 이용

  - 서비스영역과 컨트롤러 처리
    + src > main > java > org.zerock.service.ReplyService interfcae
    + src > main > java > org.zerock.service.ReplyServiceImple class

  - ReplyCOntroller의 설계
    + src > main > java > org.zerock.controller.ReplyController

  - 등록작업과 테스트

  - 특정 게시물의 댓글 목록

  - 댓글의 삭제 / 조회

  - 댓글의 수정

  - Javascript의 준비 - 모듈화

  - reply.js 댓글 등록

  - 조회 화면에서 호출

  - 댓글의 목록 처리

  - getJSON()처리 - reply.js

  - 댓글의 삭제와 갱신

  - 댓글 삭제 테스트

  - 댓글 수정/테스트

  - 특정댓글조회 / 테스트

  - 이벤트 처리와 HTML처리 
  
  - 댓글 목록의 처리

  - 새로운 댓글의 처리

  - 댓글 추가 후 처리

  - 특정 댓글의 클릭 이벤트

  - 댓글의 수정 / 삭제 처리 이벤트

  - 댓글의 페이징 처리

  - 인덱스를 이용하는 댓글 페이징 처리

  - 댓글의 수 

  - ReplyServiceImpl

  - REplyController의 수정

  - 댓글의 화면 처리

  - 댓글의 페이지 계산과 출력

  - 새로운 댓글 추가

  - 댓글의 페이지 번호 처리
