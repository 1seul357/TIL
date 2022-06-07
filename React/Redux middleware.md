# Redux middleware

### Redux 

- 정의 : 리액트 상태 관리 라이브러리. 자바스크립트 앱에서 상태(state)를 효율적으로 관리할 수 있게 도와주는 도구

- 장점

  - 컴포넌트의 상태 업데이트 관련 로직을 다른 파일로 분리시켜서 효율적으로 관리 가능
  - 컴포넌트끼리 똑같은 상태를 공유해야할 때도 손쉽게 상태값을 전달하거나 업데이트 가능
  - 코드의 유지 보수성 향상, 작업 효율 극대화
  - 미들웨어를 통해 비동기 작업을 효율적으로 관리

- 기본 개념 정리

  - 액션(Action) : 상태에 어떠한 변화가 필요할 때, 액션을 발생시켜서 변화

  - 액션 생성 함수(Action Creator) : 액션을 만드는 함수, 컴포넌트에서 더욱 쉽게 액션 발생시킬 수 있음

  - 리듀서(Reducer) : 변화를 일으키는 함수. state와 action 파라미터를 받아옴

    > 현재의 상태와 전달 받은 액션을 참고하여 새로운 상태를 만들어서 반환

  - 스토어(Store) : 현재의 앱 상태, 리듀서 등 포함되어 있음

  - 디스패치(dispatch) : 스토어의 내장함수. 액션을 발생시키는 것

  - 구독(subscribe) : 스토어의 내장함수. 함수 형태의 값을 파라미터로 받아오는 역할

- 규칙

  - 하나의 애플리케이션 안에는 하나의 스토어가 있어야 함

  - 상태는 읽기 전용이어야 함

    > 리액트에서 setState를 사용하는 것처럼 기존의 상태는 건들이지 않고, 새로운 상태를 생성하여 업데이틑 해주는 방식으로 사용해야 한다.

  - 변화를 일으키는 함수, 리듀서는 순수한 함수여야 함

    > 리덕스 함수는 이전 상태와, 액션 객체를 파라미터로 받는다.
    >
    > 이전의 상태는 건들이지 않고, 변화를 일으킨 새로운 상태 객체를 만들어서 반환한다.
    >
    > 똑같은 파라미터로 호출된 리듀서 함수는 언제나 똑같은 결과값을 반환해야 한다.

</br>
</br>

### Redux middleware

- 정의 : 리덕스가 가지고 있는 핵심 기능. 디스패치와 리듀서 사이에서의 역할

- 특징

  1. 특정 조건에 따라 액션이 무시되게 만들 수 있음

  2. 액션을 콘솔에 출력하거나, 서버쪽에 로깅할 수 있음

  3. 액션이 디스패치 되었을 때, 이를 수정해서 리듀서에게 전달되도록 할 수 있음

  4. 특정 액션이 발생했을 때 이에 기반하여 다른 액션이 발생되도록 할 수 있음

  5. 특정 액션이 발생했을 때 특정 자바스크립트 함수를 실행시킬 수 있음

- 종류 : [redux-thunk](https://github.com/reduxjs/redux-thunk), [redux-saga](https://github.com/redux-saga/redux-saga), [redux-observable](https://redux-observable.js.org/), [redux-promise-middleware](https://www.npmjs.com/package/redux-promise-middleware) 

</br>
</br>

### 리덕스 프로젝트 생성하기

```
npm config set legacy-peer-deps true
npx create-react-app learn-redux-middleware
```

```
cd learn-redux-middleware
npm i redux react-redux
```

1. 액션 타입, 액션 생성함수, 리듀서를 한 파일에 작성하는 Ducks 패턴 사용해서 counter.js 생성

   ``` javascript
   // counter.js
   
   // 액션 타입
   const INCREASE = 'INCREASE';
   const DECREASE = 'DECREASE';
   
   // 액션 생성 함수
   export const increase = () => ({ type: INCREASE });
   export const decrease = () => ({ type: DECREASE });
   
   // 초깃값 (상태가 객체가 아니라 그냥 숫자여도 상관 없습니다.)
   const initialState = 0;
   
   export default function counter(state = initialState, action) {       // 리듀서
     switch (action.type) {
       case INCREASE:
         return state + 1;
       case DECREASE:
         return state - 1;
       default:
         return state;
     }
   }
   ```

2. 루트 리듀서 생성

   ``` javascript
   // index.js
   
   import { combineReducers } from 'redux';
   import counter from './counter';
   
   const rootReducer = combineReducers({ counter });
   
   export default rootReducer;
   ```

3. 프로젝트에 리덕스 적용. src 디렉터리의 index.js에서 루트리듀서를 불러와서 이를 통해 새로운 스토어를 만들고 Provider를 사용해서 프로젝트에 적용

   ```javascript
   // index.js
   
   import React from 'react';
   import ReactDOM from 'react-dom';
   import './index.css';
   import App from './App';
   import reportWebVitals from './reportWebVitals';
   import { createStore } from 'redux';
   import { Provider } from 'react-redux';
   import rootReducer from './modules';
   
   const store = createStore(rootReducer);    // 루트리듀서 통해 새로운 스토어 만들기
   
   ReactDOM.render(
     <Provider store={store}>                // Provider 통해 적용
       <App />
     </Provider>,
     document.getElementById('root')
   );
   
   // If you want to start measuring performance in your app, pass a function
   // to log results (for example: reportWebVitals(console.log))
   // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
   reportWebVitals();
   ```

4. 프리젠테이셔널 컴포넌트 Counter.js 생성. props를 통해 number와 onIncrease, onDecrease 함수 받아오기.

   ```javascript
   // Counter.js
   
   import React from 'react';
   
   function Counter({ number, onIncrease, onDecrease }) {
     return (
       <div>
         <h1>{number}</h1>
         <button onClick={onIncrease}>+1</button>
         <button onClick={onDecrease}>-1</button>
       </div>
     );
   }
   
   export default Counter;
   ```

5. 컨테이너 만들기. Counter.js에서 버튼 클릭시 onIncrease 혹은 onDecrease 함수 실행

   > useSelector : state 조회
   >
   > useDispatch : action 발생

   ```javascript
   // CounterContainer.js
   
   import React from 'react';
   import Counter from '../components/Counter';
   import { useSelector, useDispatch } from 'react-redux';
   import { increase, decrease } from '../modules/counter';
   
   function CounterContainer() {
     const number = useSelector(state => state.counter);            // state 조회하기
     const dispatch = useDispatch();
   
     const onIncrease = () => {
       dispatch(increase());                                        // action 발생시키기
     };
   
     const onDecrease = () => {
       dispatch(decrease());
     };
   
     return (
       <Counter number={number} onIncrease={onIncrease} onDecrease={onDecrease} />
     );
   }
   
   export default CounterContainer;
   ```

6. App.js 수정

   ```javascript
   // App.js
   
   import React from 'react';
   import CounterContainer from './containers/CounterContainer';
   
   function App() {
     return <CounterContainer />;
   }
   
   export default App;
   ```

   

