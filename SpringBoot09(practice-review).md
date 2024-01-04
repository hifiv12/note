  - 업로드 결과 반환과 화면 처리
    * 업로드 결과로 브라우저에 반환해야 하는 데이터
      + 업로드된 파일의 원본이름
      + UUID값
      + 업로드된 파일의 저장 경로
    * 별도의 DTO를 구성해서 처리
      + org.zerock.mreview.dto.UploadResultDTO
  
  - ResponseEntity 반환
    * UploadController ResponseEntity(List(UploadResultDTO)) 타입으로 업로드 결과를 반환하도록 수정

  - 업로드 이미지 출력하기
    * JSON 데이터에 업로드 결과가 전송되면 화면에서는 img태그를 구성하고 해당 이미지를 보여주도록 처리
    * 이미지 데이터를 전송하는 기능을 구현

  - 썸네일 이미지 생성과 화면 처리
    * Thumbnailator 라이브러리를 이용, 업로드 후 썸네일 처리
    * 's_'로 시작하도록 파일 이름을 구성
    * Thumbnailator는 추측상 라이브러리에서 따로 올려주는거 같음 
    * 그리고 method의 get이후의 이름이 담기는 형태인듯 그래서 오타나면 콘솔창 배열 구조 안의 이름을 보고 원하는 형태로 method를 수정해야됨

  - 브라우저에서 파일 삭제

## 영화 / 리뷰 프로젝트 적용하기
  - 목표
    * 엔티티간의 연관관계와 파일 업로드 처리를 최종적으로 실습하는 목적
    * 각 계층의 구성을 확인하고, 구현
    * 기능적 요구사항
      + 영화의 등록, 수정에 파일 업로드 기능을 활용, 영화 포스터 등을 등록
      + 회원은 기존 회원이 있다고 가정
      + 회원은 특정한 영화 조회 페이지에서 평점과 자신의 감상 리뷰를 등록
      + 조회 화면에서 회원은 자신이 기록한 리뷰의 내용을 수정 / 삭제
    
  - 영화 등록 처리
    * Thymeleaf의 레이아웃 관련 / 부트스트랩 관련 파일들 추가
    * MovieController 클래스 선언
    * 등록 화면 생성
    * Movieservice / MovieServiceImpl
    * MovieController
      + post방식으로 전달된 파라미터드을 MovieDTO로 수집, MovieServie를 호출
      + 전달되는 데이터는 영화와 이미지(path, uuid, filename)들의 정보
    * 화면 처리 -> register.html
      + 첨부파일을 보여주는 div
      + Ajax를 이용해서 파일 업로드 처리
      + 결과데이터를 해당 div로 썸네일로 출력
    * 이미지 파일의 삭제와 submit 처리
      + 이미지 파일의 삭제는 Ajax를 이용해서 처리
      + submit 처리는 각 이미지를 input 태그의 히든 속성으로 구성하여 한번에 여러 개의 ImageDTO를 구성할 수 있도록 전송
        - closest() > 해당 요소에서 가장 가까운 조상요소를 선택 하며, 단하나의 선택만 리턴한다.
        - preventDefault() 
          * a, submit 태그는 특수한 기능을 가지고 있음
          * 링크이동, 새로고침 등을 막아주기 위한 메서드
    * 전체 흐름
      + 파일 업로드 > li태그 구성
      + submit 버튼 클릭 > form태그의 태그 생성
      + action > post > mapping > controller > dto 수집
      + service에서 dto > entity > db처리

  - 목록처리와 평균 평점
    * PageRequestDTO, PageResultDTO
    * MovieDTO 수정
      + 영화, 이미지들, 평점, 리뷰 개수
    * MovieService의 entityToDTO

    * 현재 리턴 부분 에러난다 ㅜㅜ

----------------------------

Spring Data JPA N + 1 해결 방법

1.join fetch
2.@EntityGraph
3.@Batch Size

  - 로그를 꼭 확인 n + 1 문제가 발생하면 위와 같은 방법으로 해결 하려고 시도.
  - 그래도 안되면 native query로
  * nativeQuery=true
    : native query에 사용된 컬럼들을 dto에 저장하는 작업이 불편
  * mybatis
    : select한 결과를 dto에 저장해 줌

---------------------

apache tika

----------------------

객체의직렬화
DTO를 JSON 형태로 내보낼려면 직렬화? 