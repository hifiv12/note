## spring mvc project > board
  - setting
    * install
      + sts ver 3.9.17
      + apache tomcat 9.0
      + jdk 11 
      + oracle 11xe
        + sqldeveloper
    * STS
      + UTF-8 : https://parkjye.tistory.com/35
      + Java 11 : https://myvelop.tistory.com/64
    * Spring legacy project
      + project name : ex02
      + templates: Spring MVC Project
      + package: org.zerock.controller
    * apache tomcat 9.0
      + Servers tap > Define a New Server
      + Apache > Tomcat 9.0 Server
        - directory : C:\Program Files\Apache Software Foundation\Tomcat 9.0
      + server > module > Path : /
  
  - pom.xml Setting
    * spring legacy project 기준 defualt에서 변경되는 사항만
    * Spring
      + java  1.8
      + org.springframeowork-version 5.0.7
    * Logging
      + log4j : 1.2.17
    * Servlet
      + javax.servlet-api : 3.1.0
    * Test
      + junit : 4.12
    * org.springframework
      + spring-test 
      + spring-jdbc
      + spring-tx
    * Hikari-cp : 2.7.8
    * ojdbc6 : 11.2.0.4
    * mybatis : 3.4.6
    * mybatis-spring : 1.3.2
    * log4jdbc-log4j2-jdbc4 : 1.16
    * lombok : 1.18.0 > scope 삭제
    * maven-comiler-plugin > configuration > source : 1.8
    * maven-comiler-plugin > configuration > target : 1.8
    * build > pugins > plug > maven-war-plugin > 3.2.0 
      + configuration > failOnMissingWebXml : false

  - DB table setting
    ```sql
      create sequence seq_board;

      create table tbl_board (
      bno number(10,0),
      title varchar2(200) not null,
      content varchar2(2000) not null,
      writer varchar2(50) not null,
      regdate date default sysdate, 
      updatedate date default sysdate
      );

      alter table tbl_board add constraint 
      pk_board 
      primary key (bno);
    ```

  - insert Dummy data
    * 아래의 sql문 으로 추가(제곱로 증가함)
    ```sql
      insert into tbl_board 
      select seq_board.nextval, title, content,  writer, regdate, updatedate from tbl_board;
      commit;
    ```
  
  - DB setting and test
    * root-context.xml
      + id : hikariConfig, class : com.zaxxer.hikari.HikariConfig
        - property(name : value)
          * driverClassName : net.sf.log4jdbc.sql.jdbcapi.DriverSpy
          * jdbcUrl : jdbc:log4jdbc:oracle:thin:@localhost:1521:XE
          * username : ora_user
          * password : hong
      + DataSource (HikariCP configuration)
        - property
          * dataSource : com.zaxxer.hikari.HikariDataSource
            + detroy-method : close
      + SqlSessionFactory : org.mybatis.spring.SqlSessionFactoryBean
        - property 
          * dataSource : dataSource
      + mybatis-spring:scan 추가 및 상단 xsi:schemaLocation, xmlns:mybatis-spring url 추가
  * project > preference > java build path > libraries > add External jars > ojdbc6.jar 추가

  - log4jdbc.log4j2.properties 
    * log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator

### 영속 계층의 처리

  - BoardVO
    * src > main > java > org.zerock.domain > BoardVO(class)
    * lombok > @Data 명시
    * 멤버변수 명시

  - Mapper Interface
    * src > main > java > org.zerock.domain > BoardMapper(interface)
    * @Select("sql")
      + sql에 쿼리를 적어놓고 그대로 불러오는가?
    * BoardMapper 테스트 
      + 불만족 오류가 나는데 알수가 없음
    
  - Mapper XML 파일
    * src > main > resources > org.zerock.mapper > BoardMapper.xml
    * getList query 작성 

  - 게시물 등록 (Create)
    * insert 기준 pk값을 알 필요가 없을 경우
    * insert문이 실행되고, 생성된 pk값을 알아야 하는 경우 -> <selectKey> 사용
      + <selectKey>
        - SQL이 실행되기 전에 별도의 PK 값등을 얻기 위해 사용
        - order='BEFORE'을 이용해서 insert구문이 실행되기 전에 호출
        - keyProperty를 통해 BoardVO.bno 값으로 set

  - BoardMapper의 insert test
    * selectkey와 비교 > 근데 뭐가 다른지 모르겠음

  - 게시물의 조회(read)
    * BoardMapper
      + read()
    * BoardMapper.xml
      + select sql 
    * BoardMapperTests
      + @Test
    
### 비즈니스 계층 구현
  
  - 비즈니스 계층(서비스 계층)
    * 고객의 요구사항을 반영하는 계층
    * 업무의 단위로 설계
      + 업무의 단위로 설계
      + 트랜잭션의 단위
    * 여러 개의 Mapper나 DAO를 사용하는 경우개 존재
    * ___Service의 형태로 작성
  
  - 서비스 패키지 설정
    * 인터페이스와 클래스를 설정하고, root-context.xml에 등록
  
  - @Service annotation
    * 스프링에 빈으로 등록되는 서비스 객체의 어노테이션
    * XML의 경우에는 <component-scan>에서 조사하는 패키지의 클래스중에 
      + @Service가 명시된 클래스의 인스턴스를 스프링의 빈으로 설정
  
  - 서비스 계층의 구현과 테스트 진행
    * 서비스 계층도 별도로 테스트 하는것이 좋음
    * 다만 하나의 Mapper, DAO를 이용하는 경우에는 테스트를 생략하는 편

### 프레젠테이션(웹) 계층의 CRUD 구현
  
  - 웹 계층의 구현
    * 웹 계층에서 가장 먼저 설계하는 것은 URI의 
    
    Task | URl | Method | Parameter | From | URL 이동
    -- | -- | -- | -- | -- | -- 
    전체 목록 | /board/list | GET | | |
    등록 처리 | /board/register | POST | 모든 항목 | 입력화면 필요 | 이동
    조회 | board/read | GET | bno | | 
    삭제 처리 | /board/remove | POST | bno | 입력화면 필요 | 이동
    수정 처리 | /board/modify | POST | 모든 항목 | 입력화면 필요 | 이동
  
  - 진행 작업의 순서 
    * 목록 페이지
    * 등록 입력/처리
    * 조회 
    * 수정/삭제

  - BoardController 목록의 처리 및 테스트
    * BoardVO의 목록을 Model에 담기
    * 테스트 코드에서 꼭 annotation이 정확히 명시되었는지 확인
    * MockMvc, MockRequestBuilders가 무엇인지
      + MockMvc : 서버에 배포하지 않고 테스트용 MVC 환경을 만들어 요청 및 전송,   응답 기능을 제공해주는 클래스
        - method
          * param / params
          * cookie
          * requestAttr
          * sessionAttr
          * content
          * header / headers
          * contentType

  - BoardController의 등록처리 및 테스트
    * POST방식으로 처리되는 데이터를 BoardVO 타입의 인스턴스로 바인딩해서 메서드에서 활용
    * BoardService를 이용해서 등록처리
    * "redirect:url"를 이용해 다시 목록으로 이동

  - BoardController의 수정/테스트
    * Redirecattributes
      + 리다이렉트 페이지를 하며 데이터를 넘기는클래스
      + method
        - addAttribute() > @RequestParam
        - addFlashAttribute() > @ModelAttribute

  - BoardController의 삭제 / 테스트

### 화면 처리
  - 화면의 처리 및 세팅
    * SB-Admin 2(MIT 라이센스)를 이용해 페이지 디자인 (다운로드)
    * src > main > webapp > resources > data, dist, js, less, pages, vendor 폴더 복붙
   
  - 목록 페이지 작성
    * 프로젝트 경로는 '/' > tomcat server module edit으로 고치기
  
  - includes 적용
    * src > main > webap > resources > 

  - list.jsp 의 적용
     * list.jsp
      + table.html에서 테이블 태그만 복사해서 붙여넣기

  - jQuery 버전 변경과 문제
    * header.jsp 
      + jquery 3.3.1 적용
    * 새로 고침 후 메뉴 펼치지는 문제
      + footer.jsp에서 해결

  - 목록 화면의 처리
    * c:forEach
    * c:out
    * JSTL
    * 중요한것!
      + BoardServiceImpl의 getList()가 현재 null을 리턴 하므로
      + DI된 mapper를 통해 List<BoardVO>를 리턴 해줘야됨 
  
  - 등록 입력 페이지와 등록
    * 기본적으로 URI에 입력되는 주소는 GET방식
    * 컨트롤러에서 @GetMapping으로 매핑, void 리턴이라면
    * WEB-INF/views 기준 밑으로 매핑된 주소 그대로 .jsp 파일을 전송
  
  - 한글 깨짐과 필터 설정
    * 등록 하고 나서 게시글이 깨지는 문제가 발생
    * web.xml을 이용하여 필터 설정과 필터 매핑을 해야됨

  - 게시물 작업 이후 재전송
    * 등록, 수정, 삭제 이후 리스트 페이지로 다시 이동
    * BoardController > RedirectAttributes.addFlashAttribute() 이용해 한번만 전송되는 데이터 저장 후 전송
    * 뷰 페이지에서 Javascript를 이용해서 경고창이나 모달창을 보여주는 형식

  - 화면의 처리
    * 컨트롤러에서 처리 후 내려줄 때 등록한 글의 번호를 result라는 이름으로 리턴함
  
  - 모달창 보여주기
    * 만약 제대로 등록되어 result가 > 0 보다 크다면 모달창을 띄우며 메세지 전송

  - 조회 페이지와 이동
    * /board/get.jsp 작성
    * BoardServiceImpl get 코드 작성
    * 리스트 페이지에서 최초로 클릭 > get으로 요청 > 상세 페이지 호출
    * 상세 페이지에서 summit 하면 

  - 게시물의 수정/삭제 처리
    * 게시물 조회 이후 수정/삭제 페이지로 이동
    * 수정 및 삭제는 Post 방식으로 처리
    * controller와 serviceImple의 modify, remove Method의 맵핑과 코드를 작성 
    * modify.jsp의 javascript 코드 작성
      + prevenDefault 를 쓰면 기존에 출력물이 다음 동작이 실행 되더라도 뷰포트에 남아 있게 하고 싶을 때 

## 오라클 DB 페이지 처리
  - order by의 고민
    * sql의 실행과정
      + sql 파싱 > 최적화 > 실행
    * sql의 처리 과정에서 데이터 정렬이 많은 경우 order by가 성능에 나쁜 영향

  - order by 대신 index

    ```sql
      select rownum rn, bno, title, content
      from tbl_board
      where rownum <= 10;
    ```

  - 식별키(pk)와 인덱스 정렬
    * primary key를 생성하면 자동으로 인덱스가 생성
    * 개발자의 의도를 힌트를 이용해 전달 > 주석 느낌인데 sql에 영향이 가는 것
  
  - ROWNUM과 인덱스
    * 테이블에서 최종적으로 나오면서 붙이는 컬럼
    * 인덱스 or FULL Scan을 통해서 나오는 ROWNUM은 다르게 나옴
  
  - 검색에 필요한 내용을 담는 Criteria 클래스
    * 기본 생성자는 1, 10 
    * 페이지 이동 시 파라미터로 받는 pageNum, amount

  - MyBatis 처리
    * BoardMapper (interface)
    * BoardMapper.xml
  
  - 페이징 처리 테스트
    * test > java > org.zerock.service.BoardServiceTests
    * assertNotNull(object) : object가 null 인지 아닌지 > message를 리턴

## 화면 페이징 처리
  - jsp 처리
    * Criteria가 추가 될 시점 BoardController, BoardService, BoarodServiceImple의 코드 다 수정완료

  - 페이지 처리에 필요한 정보들
    * src > main > java > org.zerock.domain.PageDTO (class)
  
  - jsp에서 화면 번호 출력
    * list.jsp의 table 하단에 코드 추가
    * /list 요청 할떄 model에 pageMaker라는 이름의 PageDTO가 있음
    * list.jsp에서 pageMaker의 값에 따라 페이지의 번호수를 출력함
    * 다른 기능으로 페이지 번호를 클릭 시 해당 페이지로 넘어가는 것
      + /list 요청 시 model 객체에 list라는 객체가 존재하는데 
      + controller > service > mapper 로 접근 할 당시 눌렀을때 URI의 값으로 
      + Criteria에 자동 값을 세팅 받아 해당 페이지의 번호를 눌러 mapper에게 값을 전달
      + 그럼 해당 범위만큼의 리스트를 긁어오고 그대로 model("list", 가져온 리스트)로 내려보낸다. 
      + 그럼 해당 페이지에 맞는 리스트가 출력된다. 

  - 안되는 버그들 수정