# Vue.js

##### Vue.js

- 사용자 인터페이스를 만들기 위한 자바스크립트 프레임워크
- SPA(Single Page Application) 지원
- DOM과 데이터 연결, 데이터 관리

##### SPA

- Single Page Application

- 현재 페이지를 동적으로 렌더링함으로써 사용자와 소통하는 웹 애플리케이션
- 서버로부터 최초에만 페이지를 다운로드하고, 이후에는 동적으로 DOM 구성 (필요한 부분만 동적으로 다시 작성)
- 트래픽 감소, 사용성과 반응성 향상
- 동작 원리의 일부가 CSR의 구조

##### CSR

- Client Side Rendering
- 최초 요청 시 데이터를 제외한 리소스 응답받고, 클라이언트에서는 필요한 데이터만 요청해 DOM 렌더링
- 클라이언트에서 화면 구성
- 서버와 클라이언트 간 트래픽 감소, 사용자 경험 향상 / 렌더링 시점 느림, SEO 어려움

##### SSR

- Server Side Rendering
- 서버에서 페이지 모두 구성하여 전달
- 모든 요청마다 새로운 페이지 구성
- 구동 속도 빠르고 SEO에 적합 / 트래픽 ↑, 사용자 경험 ↓

##### Nuxt.js

- Vue.js 응용 프로그램 만들기 위한 프레임 워크, SSR 지원

##### Next.js

- React 응용 프로그램을 만들기 위한 프래임 워크, SSR 지원

##### MVVM Pattern

- 애플리케이션 로직을 UI로부터 분리하기 위해 설계된 디자인 패턴
- Model, View, View Model
  1. Model : JavaScript Object. Object는 data로 사용. data 값 변경 -> DOM 반응
  2. view : DOM(HTML). 데이터 값 변경에 따라 DOM 변화
  3. ViewModel : Vue Instance. View와 Model 사이에서 데이터와 DOM에 관련된 일 처리

##### Vue.js 코드 작성 순서

- Data 로직 작성 -> DOM 작성

##### Vue instance

- Vue 인스턴스를 생성할 때는 Options객체 전달, 여러 Options들을 사용하여 원하는 동작 구현

  1. Options/DOM - el : Vue 인스턴스에 연결할 DOM 엘리먼트 필요, CSS 문자열과 HTML Element로 작성

  2. Options/Data - data : Vue 인스턴스의 데이터 객체

  3. Options/Data - methods : Vue 인스턴스에 추가할 메서드

     > interpolations과 directive에서 사용 가능, this 키워드 통해 접근 가능
>
     > 화살표 함수를 'data'에서 사용할 수 없음 (데이터와 메서드 정의)

  4. this 키워드 : Vue 함수 객체 내에서 vue 인스턴스를 가리킴


##### Template Syntax

- 렌더링된 DOM을 기본 Vue 인스턴스의 데이터에 연결할 수 있는 HTML 기반 템플릿 구문 사용
  1. Interpolation : Text, Raw HTML, Attributes, JS표현식
  
  2. Directive : v- 접두사가 있는 속성. 표현식의 값이 변경될 때 DOM에 적용
     
     > 전달인자 : <a v-bind:href="url"> 콜론을 통해 전달인자를 받을 수 있음
     >
     > 수식어 . <form v-on:submit.prevent="onSubmit"> directive를 특별한 방법으로 바인딩할 때 사용

1. **v-text** : Element를 contextText로 업데이트

2. **v-html** : Element의 innerHTML 업데이트, XSS 공격에 취약 (사용자로부터 입력받은 내용은 사용 금지)

3. **v-show** : 조건부 렌더링, Element는 항상 렌더링되고 DOM에 남음. 

4. **v-if, v-else-if, v-else** : 조건부 렌더링, directive의 표현식이 true일 때만 렌더링

   > v-show : 실제로 렌더링은 되지만 눈에만 보이지 않는 것으로, 한번만 렌더링되는 경우에는 렌더링 비용 높음. 하지만 자주 변경되는 요소라면 토글 비용 적음.
   >
   > v-if : 전달인자가 false인 경우 렌더링되지 않으며 렌더링 비용 낮음. 하지만 자주 변경되는 요소의 경우 비용 증가.

5. **v-for** : Elemets 또는 템플릿 블록을 여러번 렌더링(반복). 사용시 key 속성을 각 요소에 작성해야 함. v-if보다 우선순위 높음

6. **v-on** : Element에 이벤트 리스터를 연결. @ 사용

7. **v-bind** : HTML 요소의 속성에 Vue의 상태 데이터를 값으로 할당. : 사용

8. **v-model** : HTML form 요소의 값과 데이터를 양방향 바인딩

   > .lazy : change 이벤트 이후에 동기화
   >
   > .number : 문자열을 숫자로 변경
   >
   > .trim : 입력에 대한 trim을 진행
   
9. **Options/Data - computed** : 데이터를 기반으로 하는 계산된 속성, 함수의 반환 값이 바인딩(반환 값 반드시 있음), 종속된 데이터가 변경될 때만 함수를 실행

   > computed & methods : methods는 호출하면 렌더링을 다시 할 때마다 함수가 실행되는 반면, computed는 종속된 대상이 변경되지 않으면 함수를 여러번 호출해도 계산을 다시 하지 않고 계산되어 있던 결과를 반환한다.

10. **Options/Data - watch** : 감시하는 데이터에 변화가 일어났을 때 실행되는 함수

    > computed % watch : computed는 특정 데이터(a)를 사용/가공하여 다른 값(a)으로 만들 때 사용하며 '선언형 프로그래밍(계산해야 하는 목표 데이터 정의)'이다. watch는 특정 데이터(a)의 변화 상황에 맞춰 다른 data(increase) 등이 바뀌어야할 때 사용하며 '명령형 프로그래밍(데이터가 바뀌면 특정 함수 실행)'이다.

11. **Options/Assets - filter** : 텍스트 형식화를 적용할 수 있는 필터. interpolations 혹은 v-bind 이용할 때 사용.

##### Lifecycle Hooks

- 각 Vue 인스턴스의 초기화 단계에서 사용자 로직 실행하는 것


##### lodash library

- 모듈성, 성능 및 추가 기능을 제공하는 자바스크립트 유틸리티 라이브러리
- reverse, sortBy, range, random




