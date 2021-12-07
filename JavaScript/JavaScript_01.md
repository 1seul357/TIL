# JavaScript

##### 브라우저

- 웹 서버에서 이동하며 클라이언트와 서버 간 양방향으로 통신하고, HTML 문서나 파일을 출력하는 GUI 기반의 소프트웨어

- JavaScript는 브라우저 화면을 동적으로 만들어줌

##### DOM(Document Object Model)

- HTML, XML과 같은 문서를 다루기 위한 문서 프로그래밍 인터페이스

- 문서를 구조화하고, 구성 요소를 객체로 취급하는 논리적 트리 모델

- 속성 접근, 메서드 활용, 프로그래밍 언어적 특성을 활용한 조작

- 주요 객체

  >window : DOM을 표현하는 창, 가장 최상위 객체 (생략 가능)
  >
  >document : 페이지 컨텐츠의 Entry Point. <body> 등의 요소 포함
  >
  >navigator, location, history, screen

- DOM-해석 : 파싱. 브라우저가 문자열을 해석하여 DOM Tree로 만드는 과정

- BOM(Browser Object Model) : 자바스크립트가 브라우저와 소통하기 위한 모델. 브라우저의 창이나 프레임을 추상화해서 프로그래밍적으로 제어할 수 있도록하는 수단

##### DOM 조작

- 선택(Select) -> 변경(Manipulation)

- DOM 관련 객체의 상속 구조

  >EventTarget : Event Listener를 가질 수 있는 객체가 구현하는 DOM 인터페이스
  >
  >Node : 여러 가지 DOM 타입들이 상속하는 인터페이스
  >
  >Element : Document 안의 모든 객체가 상속하는 클래스
  >
  >Document : 웹페이지. DOM 트리의 진입점 역할
  >
  >HTMLElement : 모든 종류의 HTML 요소, 부모 element의 속성 상속

##### DOM 선택

- Document.querySelector(selector) : 선택자와 일치하는 element 하나 선택, 제공한 CSS selector를 만족하는 첫번째 element 객체 반환 (없으면 null)

- Document.querySelectorAll(selector) : 선택자와 일치하는 여러 element를 선택, CSS selector를 만족하는 인자(문자열)로 받음. NodeList 반환

- querySelector()와 querySelectorAll()을 사용하는 이유 : id, 클래스, tag 선택자 모두 사용 가능

- 선택 메서드별 반환 타입

  1. 단일 element : getElementById(id), querySelector()
  2. HTMLCollection : getElementsByTagName(name), getElementsByClassName(names)
  3. NodeList : querySelectorAll()

- HTMLCollection & NodeList 

  >배열과 같이 각 항목에 접근하기 위한 index 제공
  >
  >HTMLCollection : name, id, index 속성으로 각 항목에 접근 가능, Live Collection이므로 DOM의 변경사항 실시간 반영
  >
  >NodeList : index로만 접근 가능, querySelectorAll()에 의해 반환되는 노드리스트는 Static Collection으로 실시간 반영되지 않음

- Collection

  > Live Collection : 문서가 바뀔 때 실시간으로 업데이트, DOM의 변경사항 실시간으로 collection에 반영
  >
  > Static Collection : DOM이 변경되어도 collection 내용에는 영향을 주지 않음

##### DOM 변경

- Document.createElement() : 작성한 태그 명의 HTML 요소 생성하여 반환

- Element.append() : 특정 부모 Node의 자식 NodeList 중 마지막 자식 다음에 Node 객체나 DOMString 삽입, 여러 개의 Node 객체, DOMString 추가할 수 있음, 반환 값 없음

- Node.appendChild() : 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 Node 삽입, 한번에 오직 하나의 Node만 추가 가능(문자열 추가 불가), 추가된 Node 객체 반환

- Node.innerText : Node 객체와 그 자손의 텍스트 컨텐츠를 표현

- Element.innerHTML : 요소 내에 포함된 HTML 마크업 반환, XSS 공격에 취약

- XSS (Cross-site-Scripting) : 공격자가 웹 사이트 클라이언트 측 코드에 악성 스크립트 삽입해 공격

##### DOM 삭제

- ChildNode.remove() : Node가 속한 트리에서 해당 Node 제거

- Node.removeChild() : DOM에서 자식 Node를 제거하고 제거된 Node를 반환


##### DOM 속성

- Element.setAttribute(name, value) : 지정된 요소의 값 설정, 속성 이미 존재하면 값 갱신

- Element.getAttribute(attributeName) : 해당 요소의 지정된 값(문자열)을 반환, attributeName은 값을 얻고자 하는 속성의 이름


##### EVENT

- 네트워크 활동이나 사용자와의 상호작용같은 사건의 발생 알리기 위한 객체

- 특정 메서드 호출, 마우스 클릭 등등으로 이벤트 발생

- 특정 이벤트(type)가 발생하면, 할 일(listener)을 등록한다.

- Event handler

  - EventTarget.addEventListener() : 지정한 이벤트가 대상에 전달될 때마다 호출할 함수 설정
  
  - 이벤트 지원하는 모든 객체 Element, Document, Window 대상으로 지정 가능
  
  - EvenTarget.addEventListener(type, listener[, options])
    
    >type : 반응할 이벤트 유형
    >
    >listener : 지정된 타입의 이벤트가 발생했을 때 알림받는 객체, EventListener 인터페이스 혹은 JS function 객체(콜백 함수)여야 함
  
- Event 취소 : Event.preventDefault(). 현재 이벤트의 기본 동작 중단, 이벤트를 취소할 수 있는 경우에는 이벤트의 전파를 막지 않고 그 이벤트 취소

- 취소할 수 없는 이벤트는 event.cancelable 통해 확인