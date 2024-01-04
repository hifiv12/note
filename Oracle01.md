# Data Base
## Oracle

1. Oracle 11g Enterprise Edition 
  - 두개의 파일을 먼저 압축해제 해서 하나로 합쳐야함

- 데이터: 가공되기 전의 재료
- 정보 : 데이터를 가공해서 더 가치 있는 자료로 만든것
- IT : Information Technology
- DataBase : 데이터를 저장하는 물리적 공간
- DBMS : DataBase Management system
  * 현재는 Database의 개념
    - 작은 의미 : 데이터를 저장하는 물리적 공간
    - 넓은 의미 : DataBase + DBMS
- 고가용성(High Availability)
- 데이터베이스 소프트웨어 
  * Oracle : 은행 등 대기업에서 주로 사용
  * MS-SQL Server : 중견기업 이상에서 사용 
  * MySQL or MariaDB : 소기업~ 대기업. 오픈소스DB로 국내에서 가장 많이 사용
  * Postgresql: 대규모 데이터에 대한 성능이 좋다고 알려져서 국내 사용량이 늘어나는 추세

- No SQL
  - RDB가 아님 
  * MongoDB가 국내에서는 대표적 
    - kakao에서 일부 프로젝트부터 적극적으로 도입
    - Javascript로 코딩
  * 빅데이터에도 더 효율적

2. 
- DBA (Database Adminstrator)
  * 데이터 베이스 관리자
  * System Engineer 부류
  * DB 생성/백업/복구
  * 계정생성, 권한관리
  * 보안
- Cloud Engineer
  * 클라우드 운영자
    - AWS, MS azure, GCP
- AWS, Ms Azure
  * DB나 서버, 네트워크 등을 자유롭게 확장/축소 가능
  * 대기업은 잘 운용하면 비용 절감에 크게 도움 될 수 있음
  * 운영 시 비용을 적절하게 고려해서 선택 해야됨
    - cloud보다 hosting이 적절할 수도 있고 아닐수도 있고
    - aws 저렴버전은 aws lightsail
- on promiso
  * 서버를 cloud나 호스팅을 사용하지 않고 회사에서 직접 운영
- IDC(Internet Data Center)
  * 여러대의 서버를 통합 운영하는 센터
  * 자사용 IDC, 타사용 IDC

3. 
- it 직군
  * 01 개발자
  * 02 시스템 엔지니어
  * 03 DevOps 엔지니어
  * 대기업들은 역할이 명확
  * 스타트업 소기업들은 개발자가 2,3번도 경험
  * 주: 01, 보: 02~03 

4. 
- DB관리자가 제일 신경써야 할 일
  * 백업
  * 복구 모의 테스트 평소에 시행

- hosting
  * 자동백업이 기본제공되는 경우 많음
- cloud
  * 자동백업 설정해야됨
- 보안관제
  * 서버를 36일 24시간 모니터링

5. 데이터베이스의 구조에 따른 분류
- 계층형
- 망형
- 관계형 - Relational Database : oracle, mysql, ms-sqlserver
- 객체지향형
- RDB의 한계, 단점을 극복하고자 no SQL db이 나타남
  * mongoDB
  * 데이터가 빅데이터화 되면 RDB에서 SQL로 검색하기 힘듦

6. SQL(Strutured Query Language)
  * RDB에서 사용하는 언어
  * 기본 syntax는 대부분의 RDB에서 호환
  * 고급 SQL, 함수는 RDB마다 다름

- SQL or JAVA
  * 3~5년차 JAVA
  * 이후 SQL에 관심을 더 가짐
- table, column, row 