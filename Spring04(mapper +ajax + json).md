

---------------------------

work
  - mapper
    * root-context.xml
      + mybatis > mybatis namespace add
      + service > context namespace add
      + 

------------------------------------

paging 처리
1. Server Side Paging
  : DB에서 paging query를 사용해서 원하는 수만큼만 조회

2. Client Side Panging
  : DB에서 전체 데이터를 조회한 후, Client쪽에서 페이징 처리
  -> 데이터가 많지 않을 경우 사용 가능


------------------------------------

주소가 변경이 안되면 redirect attribute
주소가 변

------------------------------------

프로젝트 진행 순서

1. 요구사항 분석 및 기획
2. 설계
3. 구현
4. 테스트
---------------------
5. 배포
6. 유지보수


클라이언트 ajax 방식으로 서버에 요청하여 결과를 받을 때 
Json포맷을 interface로 사용하려고 한다
다음 조건을 만족하는 코드를 
Jquery로 작성하세요

서버 주소 : /list.json
json 데이터 : [
	{
    "id": "hkd,
    "name : "홍길동",
    "address" : "서울"
	},
  {
    "id": "lss,
    "name : "이순신",
    "address" : "인천"
	},
  {
    "id": "wg,
    "name : "왕건",
    "address" : "경기도"
	},
]

