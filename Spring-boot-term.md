1. JPA
2. Pageable
  - Pagnination 요청 정보를 담기 위한 Abstract interface?
  - 페이지 처리에 필요한 정보를 담게 되는 인터페이스
3. Page
  - Page<T> : 페이지 정보를 담게 되는 인터페이스
  - 주요 메서드
    * getTotalPages() : 총 페이지 수
    * getTotalElements() : 전체 개수
    * GetNumber() : 현제 페이지 번호
    * GetSize() : 페이지 당 데이터 개수
    * hasNext() : 다음 페이지 존재 여부
    * isFirst() : 시작 페이지 여부
    * getContent() : 실제 컨텐츠를 가지고 오는 메서드 List<엔티티>
    * get() : 위와 동일하나 type > Stream<엔티티>

4. 스프링에서는 매핑되어 온 뷰와 컨트롤러로 넘어오는 데이터는 파라미터에 DTO가 명시되고 거기에 자동 저장되어 진다. 

5. PageRequest
