  - 댓글 조회 기능의 분리
    * read.html 작업
    * 댓글이 추가되거나 삭제되면 화면의 갱신이 필요
    * 별도의 함수로 제작해서 사용하도록 분리
  - 댓글 추가와 모달 창
    * 댓글 추가 버튼을 클릭하면 모달 창을 보여주고 새로운 댓글을 추가할 수 있도록 구성
    * 댓글의 수정과 삭제시에도 모달 창을 이용

  - 댓글 데이터 전송
    * ajax로 보낸 데이터를 controller에서 매핑하여 내려줌

  - 댓글의 삭제 처리

  - 댓글의 수정 처리

## vscode 설정
  - start.spring.io
  - extensions
    * Excention Pack for Java
    * Lombok
    * Sprinb boot Extension Pack
## 영화 리뷰 
  - M:N 관계의 설계와 구현

  - M:N 관계의 특징

  - JPA에서 M:N 처리

  - 엔티티 클래스 설계
    * BaseEntity
    * Member
    * Movie
    * MovieImage
    * Review
  
  -  M:N Repository와 테스트
    * 테이블 구성이 완료된 후에는 Repository를 작성하고 테스트 코드를 통해서 더미데이터 추가
    * 더미데이터의 경우 매핑 테이블은 다른 테이블들의 PK를 참조하므로 마지막에 추가
    * UUID?

  - 회원과 리뷰 데이터 추가
    * blank

  - 매핑 테이블 데이터 추가

  - 필요한 데이터 정의
    * 엔티티들을 이용해서 화면등에서 필요한 데이터들을 정의
    * 목록 화면에서 영화의 제목이나 이미지 하나, 영화 리뷰의 평점/리뷰 개수를 출력
    * 영화 조회 화면에서 영화와 영화의 이미지들, 리뷰의 평균점수/리뷰 개수를 같이 출력
    * 리뷰에 대한 정보에는 회원의 이메일이나 닉네임과 같은 정보를 같이 출력

  - 페이지 처리되는 영화별 평ㄹ균 점수/리뷰 개수 구하기
    * 영화 번호 / 영화 이미지 / 영화 제목 / 리뷰 개수 / 평균 점수 순으로 출력
  
  - N + 1  문제

  - 특정 영화 조회
    * @Query() 안 sql에 파라미터가 필요한 경우 > 메서드 파라미터 앞에 @Param()으로 지정 해야 연결이 됨

  - 특정 영화 모든 리뷰와 회원 닉네임
    * @EntityGraph 를 이용하면 연관관계가 Lazy로 지정되어도 필요에 의해서 즉시 로딩(Eager) 방식으로 동작하게 지정 가능 
      + FETCH 속성값은 attributePaths에 명시한 속성은 Eager로 처리하고, 나머지는 Lazy로 처리
      + LOAD 속성값은 attributePaths에 명시한 속성은 Eager로 처리하고 나머지는 엔티티 클래스에 명시되거나 기본 방식으로 처리

## 파일 업로드의 처리
  - 서론
    * Servlet 3.0 버전부터는 별도의 라이브러리 없이도 Servlet API만으로 파일 업로드 처리가 가능
    * 파일 업로드 기능 자체의 어려움보다는 이에 대한 저장/삭제 등이 관건
    * 이미지의경우 반드시 섬네일 파일을 같이 생성
  
  - 파일 업로드를 위한 설정
    * WAS가 Servlet3이상의 API를 지원하는 경우
    * application.properties
      ```application.properties
        spring.servlet.multipart.enabled=true
        spring.servlet.multipart.location=C:\study\spring-boot-workspace\mreview
        spring.servlet.multipart.max-request-size=30MB
        spring.servlet.multipart.max-file-size=10MB
      ```
    
  - 컨트롤러와 테스트 화면
    * org.zerock.mreview.controller.UploadController 생성
      + 파일 업로드를 처리하는 별도의 컨트롤러 추가
    * org.zerock.mreview.controller.UploadTestController 생성
      + 사용자가 파일을 업로드할 수 있는 화면을 제공하는 컨트롤러
    * uploadEx.html 생성
      + ajax 업로드 처리
  
  - 업로드 된 파일의 저장
    * MultipartFile 객체를 이용해서 파일 데이터 처리
    * transferTo()를 이용하면 간단히 파일 저장 가능
    * 파일 저장 단계에서 고려사항
      + 업로드된 확장자가 이미지만 가능하도록 검사
      + 동일한 이름의 파일이 업로드 된다면 기존 파일을 덮어쓰는 문제
      + 업로드 된 파일을 저장하는 폴더의 용량

  - 업로드 관련 문제 해결
    * application.properties 내의 역슬래시
      + \\로 사용하는 것을 일반 디렉토리 주소 처럼 백슬래시 / 로 변경하면 된다
    * 동일한 이름의 파일 문제
      + UUID 혹은 현재 시간 등을 이용해서 중복된 파일이 없도록
    * 동일한 폴더에 너무 많은 파일 문제
      + '년/월/일'과 같이 폴더를 구분해서 저장하는 방식을 이용
    * 파일의 확장자 체크
      + 서버 뿐 아니라 클라이언트에서도 전송되는 파일의 확장자를 체크 

---------------------------

영화 : 회원
N : M

하나의 영화에 여러 회원이 리뷰를 달 수 있다.
한명의 회원이 여러 영화에 리뷰를 달 수 있다.

영화에 회원이 리뷰를 단다

학생이 도서를 대출한다

회원이 상품을 주문한다

M : N => 1:N, M:1로 구현

영화 리뷰 회원
  1 : N, M : 1

-----------------------------

구동 / 부팅
외부 장치 인식
ROM 
