# 리덕스

### 리덕스 미들웨어

- 정의 : 리덕스가 가지고 있는 핵심 기능

- 특징

  1. 특정 조건에 따라 액션이 무시되게 만들 수 있음

  2. 액션을 콘솔에 출력하거나, 서버쪽에 로깅할 수 있음

  3. 액션이 디스패치 되었을 때, 이를 수정해서 리듀서에게 전달되도록 할 수 있음

  4. 특정 액션이 발생했을 때 이에 기반하여 다른 액션이 발생되도록 할 수 있음

  5. 특정 액션이 발생했을 때 특정 자바스크립트 함수를 실행시킬 수 있음

- 종류 : [redux-thunk](https://github.com/reduxjs/redux-thunk), [redux-saga](https://github.com/redux-saga/redux-saga), [redux-observable](https://redux-observable.js.org/), [redux-promise-middleware](https://www.npmjs.com/package/redux-promise-middleware) 



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
   
   export default function counter(state = initialState, action) {       // dispatch 통해 액션 발생시 해당 함수 실행
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

   

