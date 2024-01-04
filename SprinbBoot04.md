  - exSidebar.html
    * th:replace 의 주소가 절대 경로로 되어 있는데 이것을 상대 경로로 고쳐야함
  
  4. 프로젝트 구조 만들기
    - 프로젝트의 계층별 구조와 객체들의 구성
    - Querydsl을 이용하는 동적으로 JPQL처리하기
    - Entity객체와 DTO처리
    - 화면에서 페이징 처리

    - 프로젝트의 와이어 프레임
      * 페이지
        + GuestBook List Page
        + GuestBook Register Page
        + GuestBook Read Page
        + GuestBook Modify Page
      * URL
        + /guestBook/list > get, 목록
        + /guestBook/register >get, 입력 화면
        + /guestBook/register > post, 등록 처리 > /guestbook/list 
        + /guestBook/read  > get, 조회 화면
        + /guestBook/modify > get, 수정 화면
        + /guestBook/modify > post, 수정 처리 > /guestbook/read
        + /guestBook/remove > post, 삭제 처리 > /guestbook/list
    - 프로젝트의 기본 구조
      * view : Thymeleaf page
      * Controller : GuestbookController
      * Service : GuestbookService, GuestbookServiceImpl
      * Repository : GuestBookRepository

    - DTO and Entity
      * dto는 Service <-> Controller 계층 사이
      * Entity는 Service <-> Repository 계층 사이

    - 프로젝트 생성
      * start.spring.io
        + gradle-groovy
        + java 11
        + group : org.zerock
        + artifact : guestbook
        + dependencies
          - spring web
          - lombok
          - spring boot devtools
          - thymeleaf
          - spring data jpa
      * gradle 버전이 맞지 않을 경우 
        + gradle > wrapper > gradle-wrapper.properties
        + distributionUrl 에 명시된 gradle 버전 수정
      * build.gradle 추가
        + mariadb-java-client 3.1.4
        + thymeleaf-extras-java8time 3.0.4
      * application.properties

  - 컨트롤러 / 화면 준비
    * 레이아웃 적용 준비
    * 컨트롤러 패키지와 컨트롤러 클래스 추가

  - 자동으로 처리되는 날짜 / 시간 설정
    * Entity의 등록시간과 수정 시간에 대한 설정을 위한 클래스를 구성
    * @EnableJpaAuditing 어노테이션 적용 ? 
      + Entity의 Persist?, Remove, Update, Load에 대한 event 전과 후에 대한 콜백 메서드 제공하는 어노테이션
    * @EnableJpaAuditing
      +  JPA 에서 auditing 을 가능하게 하는 어노테이션
      + JPA auditing : 모든 요청과 응답에 누가, 언제 접근했는지 하나의 엔티티로 관리
    * @CreateDate
      + 인스턴스가 생성되는 것을 감지하고 그 시간을 저장
    * @LastModifiedDate
      + 인스턴스가 수정되는 것을 감지하고 그 시간을 저장
    * @MappedSuperClass
      + 엔티티의 공통 매핑 정보가 필요할 때 

  - 엔티티 클래스와 Querydsl
    * 다양한 상황에 맞게 동적으로 JPQL을 생성하는 방법
    * JOOQ나 Querydsl이 주로 사용
    * Querydsl의 경우 별도의 Q도메인이라는 클래스를 생성
    * 동적으로 쿼리를 작성할 때 Q도메인을 이용?
  
  - 리포지토리 작성
    * JpaRespository 상속

  - 동적 쿼리 처리를 위한 querydsl 설정
    * www.querydsl.com의 JPA를 이용해서 처리
    * build.gradle에 plugins 추가
    * build.gradle 파일에 라이브러리 추가
    * Gradle의 task 추가

  - gradle의 task 생성
    * build.gradle
      + 현재 스프링 부트 버전은 2.7 이상 
      + 실습 코드는 2.3 > querydsl 4.. 버전
      + queryldsl의 버전이 지원이 안되는 상황
        - 스프링 부트 2.6, Querydsl 5.0 지원방법
        
        ```gradle
          buildscript {
            ext {
                queryDslVersion = "5.0.0"
            }
          }

          // dependencies에 querydsl 추가 
          implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
          annotationProcessor "com.querydsl:querydsl-apt:${queryDslVersion}"
        ```
      - 나머지는 실습 코드와 동일하게 진행

  - querydslPredicatedExecutor 추가 (GuestbookRepository 다중 상속)

  - 엔티티 테스트
    * src > test > java > org.zerock.guestbook.repository.GuestbookRepositoryTests
  
  - 수정 시간 테스트
    * Guestbook 수정
    * 안됨..

  - Querydsl 테스트
    * 제목/내용/작성자 중 단하나만 검색
    * 위의 사항 중 2가지를 조합해 검색
    * 위으 사항 전부를 조합해 검색

  - 단일 항목 검색 테스트
  - 다중 항목 검색 테스트

  - 서비스 계층과 DTO
    * DTO를 이용하는 이유
      + JPA의 경우 엔티티 객체가 단순한 객체가 아니라 영속 컨텍스트에 영향을 받는 객체이므로 DTO로 처리하면 순수한 데이터를 사용하는 것이 가능
      + 엔티티 객체는 가능하면 불변을 유지하는 것이지만 DTO는 가변
      + 검증(validate)이나 화면에 필요한 추가적인 기능들을 사용 가능
      + 엔티티 클래스와 유사하게 작성되므로 코드의 양이 늘어나는 단점

  - 등록과 DTO를 엔티티로 변환하기
    * 가능하면 DTO Class, Entity Class가 독립적으로 처리할 수 있도록 서비스 계층에서 변환
    * GuestService > GuestServiceImpl
  
  - 목록 처리
    * 화면 처리에 필요한 Entity들을 DTO로 변환
    * DTO타입의 Pageable 객체 처리 필요

  - 목록을 처리하는 DTO
    * Page type Guestbook -> GuestBookDTO로 변환
    * 페이지 번호, 검색 조건등의 처리는 PageRequestDTO라는 별도의 DTO를 작성해서 처리

  - 페이지 결과 처리 DTO
    * Page<엔티티> 로 나오는 결과를 DTO의 목록으로 변환하고, 결과를 화면까지 전달하기 위해서 PageResultDTO라는 클래스를 설계
    * DTO의 리스트와 페이지 구성에 필요한 정보를 파라미터로 받아서 처리할 수 있도록 구성
    * 다양한 상황에서 사용하기 위해서 타입은 제네릭으로 처리하고 java.util.Function을 이용해서 유연한 구조로 처리

  - 서비스 계층에서 목록처리
    * GuestbookService
    * GestbooksServiceImpl
  
  - 목록 데이터의 페이지 처리
    * Page<엔티티> 내부에는 페이지 처리에 필요한 많은 정보들이 존재하므로 이를 이용
    * PageResultDTO에서는 페이지 궛ㅇ에 필요한 정보들을 정의하고 이를 추출해서 사용
      + start
      + end
      + prev, next
      + page

  - 페이지 번호의 계산
    * 현재 페이지를 기준으로 화면에 출력되어야 하는 마지막 페이지 번호를 우선 처리
    * 화면의 시작 페이지 번호는 tempEnd - 9;
    * 실제 데이터가 부족한 경우를 위해 마지막 페이지 번호는 전체 데이터의 개수를 이용해서 다시 계산
    * 기타 필요한 이전 페이지 여부 / 다음 페이지 존재 여부 계산
  - 컨트롤러와 화면 처리

  - 등록 페이지와 등록처리

  - 방명록의 조회 처리

  - 방명록 수정과 삭제

  - 검색 처리

  

  -------------------------------

  실력있는 개발자는 복잡한것도 쉽게 풀고
  그렇지 않은 개발자는 쉬운것도 복잡하게

  함수를 만드는 경우
  1.같은 코드를 반복적으로 사용할 때 > 무조건
  2.어떤 기능을 담당하는 코드를 다음 프로젝트에도 또 사용할 것 같은 때 > 권장
  3.어떤 기능을 담당하는 코드를 구분해 놓고 싶을 때 > 마음대로

  -> 함수와 클래스를 무조건 많이 만드는 것은 좋은 코드가 아니다.
  -> 클래스 안의 멤버들이 서로 연관성이 있는지 고민.

펌웨어
: 부팅과관련 
ex> PC의 BIOS

임베디드
: H/W에 S/W를 내장 시킨다
ex> 아두이노에서 C언어로 코딩을 해서 아두이노에 embedded

드라이버
: 외부장치. 주변장치를 인식해서 사용할 수 있게 해주는 S/W
ex> MP3드라이버, 스마트폰 드라이버, 그래픽카드 드라이버

램 썼다가 지우고
롬은 안지워짐
 
-> HW 컨트롤 공통점

pdfN
18~20 page ?
48 page C, C++로 코딩한다.
55~57 page bootloader 만들기 작업
67 page 명령어 쓰는법 체크