## mvc 패턴 구조
  1. Table
  2. DTO
  3. DAO(crud)
  4. Controller
  5. View (jsp)

## 데이터베이스 종류
  - NoSQL
    * MongoDB
    * 장단점
      + 대용량 데이터 처리에 유리함 
      + 트랜잭션 처리가 불편
      + 참조 처리 불편, 그대신 빠른 처리 속도
  - 데이터베이스의 특징 비교 
    * 오라클 : 적용 규모 대규모
  - common-beanutils

네이버 구멍가게 코딩단 카페

Spring tools 4 -> spring boot 용
Spring tools 3 suit -> spring 용

maven
  : 빌드 도구, 라이브러리 형상관리
  -> pom.xml에 라이브러리를 등록하면, maven이 MVNRepository에서 다운로드 하여 등록
  -> 협업시 pom.xml을 팀원끼리 공유. 모든 팀원이 같은 라이브러리 버전으로 개발 가능
