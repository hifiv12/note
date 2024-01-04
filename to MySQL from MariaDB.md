## maria db 에서 mysql로 갈아타기
  - 현재 jump to spring의 2장 14강에서 교체를 하는 것입니다.
    * 해당 버전 이전까지는 H2 DB에서 MySql로 교체하는 것을 시도 해보시길 바랍니다.
  - MySql WebBench sql version check

    ```sql
      select version();
    ```
    * 위의 명령어로 버전 확인 가능 
    * 다만 현재 조회시 mariaDB 10.x 버전으로 확인
  - 목적은 MySql Server로 변경
    * 윈도우 시작 메뉴 > 서비스 검색
    * 서비스 목록 중 mariaDB 서비스 종료
    * 서비스 목록 중 mysql 5.7 버전 서비스 실행
  
  - 이후 sbb 프로젝트에서 mysql 로 변경하는 방법 
  
    * MySql WebBench
      + 기존에 만들어져 있던 root 계정으로 들어가서 아래의 sql을 작성

      ```sql
        /*test_db database 생성*/ 
        create database test_db;

        /*
        사용자 생성 
        @localhost는 로컬에서만 접속가능
        identified by : 비밀번호
        */
        create user 'tester'@'localhost' identified by 'test';
        /*
        test_db에게 모든 권한을 위임 * 애스터리크는 db안의 모든 테이블을 의미
        */
        grant all privileges on test_db.* to 'tester'@'localhost';
        flush privileges;
      ```
    * build.gradle

      ```build.gradle
        implementation 'mysql:mysql-connector-java:8.0.32'
      ```
    * application.properties
      ```application.properties
        # DATABASE
        ## Mysql jdbc driver 설정
        spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
        ## DB Source URL 설정
        ### 보안과 encoding 문제로 추가됨 1)useSSL=false 2) &characterEncoding=utf8
        spring.datasource.url=jdbc:mysql://localhost:3306/test_db?useSSL=false&useUnicode=true&serverTimezone=Asia/Seoul&allowPublicKeyRetrieval=true&characterEncoding=utf8
        ## DB 사용자 이름 설정
        spring.datasource.username=tester
        ## DB 사용자 암호 설정
        spring.datasource.password=test
        ## true 설정 시, JPA 쿼리문 확인 가능
        spring.jpa.show-sql=true
        ## DDL(create, alter, drop) 정의 시, DB의 고유 기능을 사용
        spring.jpa.hibernate.ddl-auto=update
        ## JPA의 구현체 Hibernate가 동작하면서 발생한 SQL의 가독성 높임
        spring.jpa.properties.hibernate.format_sql=true

        spring.thymeleaf.prefix=classpath:/templates/
        spring.thymeleaf.suffix=.html
      ```

  - 이후 sbb test class로 이동 후 잘 돌아가는지 check

  @Controller
@RequestMapping("/answer")
@RequiredArgsConstructor
public class AnswerController {

    private final QuestionService questionService;
    private final AnswerService answerService;

    
    //매개변수에 붙은 id, content값들은 question_detail.html의 ${}의 값을 가져오는 것임으로 이름을 같게 해주셔야합니다.
    //id값은 list에서 처음에 값을 List형태로 값을 다 가져온 것에서 detail페이지로 넘어갈 때 해당 List인덱스의 id값을 가져온 값이 들어가 있음
    //그 id값이랑 question_detail.html파일의 content에 적은 값을 가지고 service의 create함수(답변저장해주는거임) 호출 후 return의 주소값으로 이동
    @PostMapping("/create/{id}")
    public String createAnswer(Model model, @PathVariable("id") Integer id, @RequestParam String content){
        Question question = this.questionService.getQuestion(id);
        this.answerService.create(question, content);
        return String.format("redirect:/question/detail/%s", id);
    }
}
주석의 설명방식이 쉽진 않아 보여 흐름을 정리 하려고 답변 답니다.
1. question_list.html 에서 get method를 통해 id 값을 전달, Question Controller의 해당 매핑 메서드의 파라미터로 전달 
2. Question Controller 실행문 중 서비스를 이용, id값을 통해 Question 객체를 DB에서 불러와 저장
3. model 객체 안 question이란 이름으로 response를 내립니다.
4. question_detail.html는 받은 response 안에서 question이라는 객체를 thymeleaf 문법을 통해 해당 정보를 뿌리게 됩니다.
5. 이후 답변을 작성 할때 post method를 통해 parameter를 전달하게 되는데, 이때 AnswerContrller의 해당 주소 매핑이 되어 있는 메서드 parameter를 받는 방법 중
  - URI을 통해 온 값을 가져올 때는 PathVariable("id") _자료형 _변수명 으로 파라미터를 세팅하게 됩니다. 그럼 스프링에서 자동적으로 파라미터를 세팅합니다.
6. 해당 컨트롤러의 메소드 실행문 중 전달받은 id값으로 해당 Question객체를 불러오고 answerService를 통해 Question 객체와, 같이 전달받은 Content를 create 메서드를 통해 db에 저장합니다.
7. 실행문이 끝나고 난 뒤 "redirect:/question/detail/"+id 값을 통해 해당 detail 페이지로 리다이렉트 시킵니다. 
