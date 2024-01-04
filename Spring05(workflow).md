## Spring mvc project work flow
1. 테이블 생성
  - oracle sqldeveloper
2. VO 생성
  - src > main > java > org.zerock.domain > BoardVO.java
    + @Data > lombok 설치 후 어노테이션
    + 멤버 변수 설정
3. Mapper 세팅
  - src > main > java > org.zerock.mapper > BoardMapper.java
  - src > main > resource > org.zerock.mapper.BoardMapper.xml
    + mapper namespace 명시
  - BoardMapper.java interface에 정의된 method의 이름과 BoardMapper.xml 내의 태그 id 와 일치 시킴
  - 각 태그명에 맞는 태그내용을 sql문 작성
4. Service 세팅
  - src > main > java > org.zerock.service > BoardService.java (interface)
  - src > main > java > org.zerock.service > BoardServiceImpl 
    + BoardService 를 상속
    + @Setter(onMethod_ = @Autowire)
      - lombok에 의한 자동 의존성 주입
  - method의 파라미터에 적힌 dto는 mapper와 연동되어 자동으로 받아온 데이터가 저장되어 있음
5. Controller
  - src > main > java > org.zerock.controller > BoardController.java
    + 컨트롤러 실행시 lombok에 의해 생성자 의존성 주입이 자동
      + AllArgsConstructor와 같이 사용
  - 컨트롤러가 서비스를 호출 
    + BoardService(interface)의 method를 호출 
    + BoardServiceImple의 호출 
    + BoardMapper.java 호출
    + BoardMapper.xml 호출
    + DB 쿼리 실행
    + 최초 실행한 컨트롤러 method에 데이터를 가공
    + model.addAttribute("변수" , 서비스호출)



------------------------------------------------

db sql index 장점
- sort
- rowid가 적혀 있음
- 속도가 빠르다

Query Hint
  - 쿼리 옵티마이저가 쿼리문을 분석해서 실행계획을 작성
  - Query Hint는 쿼리옵티마이저가 분석한 대로 실행하지 말고, 개발자가 작성한 Query Hint대로 강제로 실행하도록 함.