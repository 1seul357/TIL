# Vue

##### vuex

- 상태 관리 패턴 + 라이브러리
- 상태(state)를 전역 저장소(store)로 관리할 수 있도록 지원하는 라이브러리
- 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소
- 동일한 state를 공유하는 다른 컴포넌트들도 동기화

##### vuex(2)

- State

  > 중앙에서 관리하는 모든 상태 정보(data)
  >
  > 각 애플리케이션마다 하나의 저장소만 갖게 됨
  >
  > 각 컴포넌트는 Vuex Store에서 state 정보를 가져와서 사용

- Mutations

  > state를 변경하는 유일한 방법
  >
  > handle는 동기적임(비동기적 로직은 state가 변화하는 시점이 의도한 것과 달라질 수 있고, 콜백이 실제로 호출될 시기를 알 수 없음)
  >
  > 첫번째 인자로 state를 받고, Actions에서 commit( ) 메서드에 의해 호출

- Actions

  > 비동기 작업 포함
>
  > Context 객체 인자 받음, 컴포넌트에서 dispatch( ) 메서드에 의해 호출
>
  > Actions를 통해 state를 조작할 수 있지만 하지 않음
>
  > -> 명확한 역할 분담을 통해 규모가 커졌을 때, state를 올바르게 관리하기 위해서

- Getters

  > state를 활용하여 계산 수행, 실제 상태를 변경하지는 않음
  >
  > getters의 결과는 state 종속성에 따라 캐시되고, 종속성이 변경된 경우에만 재계산

##### Compontent Binding Helper

- 배열 조작을 편하게 할 수 있도록 하는 것

- mapState : Computed와 State를 매핑. state를 객체 전개 연산자로 계산하여 추가

- mapGetters : Computed와 State를 매핑. getters를 객체 전개 연산자로 계산하여 추가

- mapActions : actions를 객체 전개 연산자로 계산하여 추가

- mapMutations

##### LocalStorage

- Vuex state : Vuex state를 자동으로 브라우저의 LocalStorage에 저장해주는 라이브러리

- 페이지가 새로고침 되어도 Vuex state를 유지시킴


##### actions 없이 mutations으로만 state를 변경해도 되는가?

- 변경할 수 있다. 하지만 저장소의 각 컨셉은 역할이 존재하도록 설계되어 있다.