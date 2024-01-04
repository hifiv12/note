  - JList
    * 여러 개의 아이템을 리스트 형식으로 보여주고 선택하는 컴포넌트
    * JList<E>
    * 생성자
    * 수정
      + JList<E>.setListData()
      + 같은 타입의 배열을 만들어 데이터 값을 추가
      + 위의 함수를 이용해 레퍼런수 변수 삽입

  - JCombobox<E>
    * 텍스트 필드, 버튼, 드롭다운 리스트로 구성
    * Action Event
      + 콤보박스 의 아이템 선택시 Action이벤트 발생
      + 주요 메소드
        - getSelectedIndex() 인덱스 리턴
        - getSelectedItem() 객체 레퍼런스 리턴

  - JSlider
    * 마우스로 움직이면서 값을 선택하는 컴포넌트
    * 제어
      + 슬라이더 방향 설정
        - setOrientation(int orientation)
      + 최대 최소 값 설정
        - setMaximum(int max) / min
      + label 보이기/감추기
        - setPaintLabels(boolean b)
      + tick 보이기/감추기
        - setPaintTicks(boolean b)
      + track 보이기/감추기
        - setPaintTrack(boolean b)
      + 큰 눈금 간격 지정
        - setMajorTickSpacing(int space)
      + 작은 눈금 간격 지정
        - setMinorTickSpacing(int space)
      + 슬라이더 값 제어
        - setVaule(int n)
    * 이벤트 
      + JSlider 값이 변경되면 발생
      + ChangeListener 메소드
        - stateChanged(ChangeEvent e)


12. 그래픽
  - 스윙 컴포넌트 그리기
    * paintComponent(Graphics g)
      + 모든 스윙 컴포넌트가 이 메소드를 가짐
    * Graphics 객체
      + 컴포넌트 그리기에 필요한 도구를 제공하는 객체 

  - 그래픽 기반 GUI 프로그래밍
    * 스윙 컴포넌트를 사용않고 선, 원, 이미지를 직접 GUI 화면 구성
    * 장점
      + 자유로움
      + 컴포넌트 그리기보다 빠름
      + 자바 GUI 기술 이해 도움
  
  - Graphics
    * x, y축 좌표 체계
    * 기능
      + 색상 선택
      + 문자열 출력
      + 도형 그리기 / 칠하기
      + 이미지 출력
      + 클리핑 

  - Color and Font class
    * color(int r, int g, int b)
      + Color.BLUE or new Color(r, g, b)
    * font(String fontFace, int style, int size)
      + setFont / setColor / drawString

  - shape draw and paint
    * 메소드
      + drawLine
      + drawOval
      + drawRect
      + drawRoundRect

  - Graphics 이미지 그리기
    * 원본 크기로 그리기
    * 크기 조절하여 그리기
    * 원본의 일부분 크기 조절하여 그리기

  - 클리핑
    * 클리핑 영역에서만 그래픽이 이뤄지도록 하는 기능
    * 영역 설정
      + setClip(int x, int w, int h)
      + clipRect(int x, int y, int w, int h)


-------------------------------------------------------

