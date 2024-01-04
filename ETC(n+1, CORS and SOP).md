n+1 해결법
1.fetch join
2.@EntityGraph
  -> fetch join시 @OneToMany paing처리를 하면 전체데이터를 가져와서 메모리에 올려두면 페이징 처리하기가 쉬움
  => @BatchSize(size = 100)를 사용
  @ManyToOne에서 페이징 처리는 limit 사용해서 정상적으로 이루어짐

ChainedTransactionManager
  : DB가 서로 달라서 Tansaction을 하나로 묶을 때 사용
  : DataSource가 다를 때 하나의 Transaction
서로 다른 connection에서 jpa, mybatis가 따로 실행될 때

---------------------------

## CORS and SOP
  - 출처
    * URL주소중 Protocol, Host, 포트를 합친것, 즉 서버의 위치를 찾아가기 위한 기본 주소
    * 포트번호 생략 가능
  - SOP(Same-Origin-Policy)
    * 같은 출처에서만 리소스를 공유할 수 있다라는 정책
    * XMLhttpRequest, Fetch API
    * 다른 도메인의 소스에 대해 자바스크립트 ajax 요청 API 호출
    * 웹 폰트 CSS 파일 내 @font-face에서 다른 도메인의 폰트 사용시
  - CORS
    * Cross-Origin 정책을 지원
      * link, img, script, video 
