  - @Contoller : 해당 클래스의 인스턴스를 스프링의 빈으로 등록하고 컨트롤러로 사용

  - @RequestMapping : 특정한 URI에 대한 처리를 해당 컨트롤러나 네서드에서 처리

  - RequestMapping의 변화
    * 4.3 before : @RequestMapping(method ="get")
    * 4.3 after : @GetMapping, @PostMapping으로 간단히 표현

  - 컨트롤러의 파라미터 수집
    * spring controller는 메서드의 파라미터를 자동으로 수집, 변환하는 기능 제공
    * Java Beans 규칙에 맞게 작성
      + 생성자가 없거나 빈 생성자
      + 올바른 규칙으로 만들어진 Getter/Setter

  - 컬렉션
    * @RequestParam("name") ArrayList<String> name

  - @InitBinder
    * ?

  - @DataTimeFormat
    * 날짜에 대한 처리가 쉽게 추가되 어노테이션

  - Model이라는 데이터 전달자
    * Model Object : JSP 컨트롤러에서 생성된 데이터를 담아서 전달하는 역할을 하는 존재
    * 모델 2 방식에서 사용하는 request.setAttribute()와 유사

  - @ModelAttribute
    * 컨트롤러에서 메서드의 파라미터는 기본 자료형을 제외한 객체형 타입은 다시 화면으로 전달
    * @ModelAttribute는 명시적으로 화면에 전달되도록 지정

  - RedirectAttribute
    * 화면에 한번만 전달되는 파라미터를 처리하는 용도
    * 내부적으로 HttpSession객체에 담아서 한번만 사용되고, 폐기
  
  - Controller의 리턴타입
    * String
      + 상황에 따라 다른 화면을 보여줄 필요가 있을 경유에 유용하게 사용
      + redirect, forward의 키워드를 붙여서 사용가능
    * void
      + 호출하는 url과 동일한 이름의 jsp파일
    * 객체 타입
      + XML or JSON으로 처리
      + @ResponseBoby 와 같이 사용 
    * VO, DTO
      + 주로 JSON 타입의 데이터를 만들어서 반환하는 용도로 사용(특정 라이브러리 필요) 
    * ResponseEntity
      + HTTP 헤더 정보와 추가적인데이터를 전달할 때 사용
    * Model, MOdelAndView
      + Model로 데이터를 반환하거나 화면까지 같이 지정하는 경우
    * HttpsHeaders
      + 응답에 내용 없이 Http 헤더 메시지만 전달하는 용도로 사용

  - 파일 업로드
    * Servlet 3.0 이후 (tomcat 7.0)에 기본적으로 업로드 되는 파일을 처리할 수 있는 기능 추가
    * commons-fileupload 라이브러리 등을 사용
    * servlet-context.xml 에 multipartResolver 빈 설정
    * html <form> 태그 enctype='multipart'
  
  - 컨트롤러의 예외(Exception) 처리
    * @ExceptionHandler + @COntrollerAdvice를 이용한 처리
      + @ControllerAdvice
        - 예외 처리와 원래의 컨트롤러가 혼합된 형태의 클래스가 작성되는 방식
        - @ExceptionHandler(class...) 에 들어가는 클래스가 예외타입을 처리한다는 으미
    * @ResponseEntity 를 이용한 예외 메세지 구성


----------------------------

주소와 다른 값을 가지고 이동 할떄는 리턴값을 가지고
주소와 같은 값으로 이동없이 할떈 void

controller의 parameter가 dto나 객체인 경우
  -> instance가 자동생성됨
  -> 이전 화면에서 넘어오는 데이터가 있으면 자동으로 수집됨

@ResponseBody
  -> ajax처리를 위한 매핑

4.12.01
  -> 4 : marjor version number
  새로운 기능이 대폭 추가 됐을 때 변경
  -> 12 : minor version number
  기능이 일부 수정/삭제 되거나 추가 됐을 때 변경
  -> 01 : fatch number
  버그가 수정되거나, 오류가 개선되거나

primary key를 만들면 자동으로 index가 생성됨

select * from tbl_board;
  -> 인덱스가 사용 안됨

select *
  -> bno가 pk이므로 index가 생성되고, where 절에 bno가 사용되므로 index를 사용할 가능성이 높다.