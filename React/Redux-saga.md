# Redux-saga

### redux-saga

- 정의 : 액션을 모니터링하고 있다가, 특정 액션이 발생하면 이에 따라 특정 작업을 하는 방식

  > 특정 작업 : 특정 자바스크립트 실행, 다른 액션을 디스패치, 현재 상태 불러오는 것

- 특징

  - 비동기 작업을 할 때 기존 요청 취소 처리 가능
  - 특정 액션이 발생했을 때 이에 따라 다른 액션이 디스패치되게끔 하거나, 자바스크립트 코드를 실행
  - 웹소켓을 사용하는 경우 채널이라는 기능을 사용하여 더욱 효율적으로 코드 관리
  - API 요청이 실패했을 때 재요청하는 작업 가능



### Generator

함수에서 값을 순차적으로 반환 가능

```javascript
function* generatorFunction() {
    console.log('안녕하세요?');
    yield 1;
    console.log('제너레이터 함수');
    yield 2;
    console.log('function*');
    yield 3;
    return 4;
}

const generator = generatorFunction();              // 제너레이터 생성
generator.next()                                    // 제너레이터 호출
```

- fuction* : 제너레이터 함수 만들 때 fuction* 키워드 사용

- 제너레이터 함수 호출 시 반환되는 객체가 제너레이터

  > 호출 시 인자 전달하여 제너레이터 함수 내부에서 사용할 수 있음

- 제너레이터 호출 시 yield 값 반환하고 코드의 흐름 멈추게 됨

  > yield : generator에서 사용하는 중단지점



### Generator로 액션 모니터링

```javascript
function* watchGenerator() {
    console.log('모니터링 시작!');
    while(true) {
        const action = yield;
        if (action.type === 'HELLO') {
            console.log('안녕하세요?');
        }
        if (action.type === 'BYE') {
            console.log('안녕히가세요.');
        }
    }
}

const watch = watchGenerator();

watch.next()

watch.next({type: 'HELLO'});

watch.next({type: 'BYE'});
```

액션을 모니터링하면서 특정 액션(watch.next({type: 'HELLO'});)이 발생했을때 자바스크립트 코드 실행



### 리덕스 사가 effect에서 자주 쓰이는 함수

- call : 함수의 동기적인 호출을 할 때 사용
- fork : 함수의 비동기적은 호출을 할 때 사용, 순서와 상관없이 실행해야할 때 사용
- put : 액션 함수 (dispatch)로 진행시킬 때 사용
- takeEvery : 모든 액션을 유효하게 인정 (디스패치되는 모든 액션 처리)
- takeLatest : generator 함수에서 마지막 액션 하나만 유효하게 인정하고 싶을 때 사용 (디스패치된 가장 마지막 액션만 처리)



### 리덕스 사가 설치 및 비동기 카운터 만들기

`npm i redux-saga`

1. counterSaga 함수를 통해 INCREASE_ASYNC, DECREASE_ASYNC  액션 모니터링

   > counterSaga 함수는 다른 컴포넌트에서 불러와서 사용할 것이기 때문에 export 키워드 사용

```javascript
// modules/counter.js


import { delay, put, takeEvery, takeLatest } from 'redux-saga/effects';

// 액션 타입
const INCREASE = 'INCREASE';
const DECREASE = 'DECREASE';
const INCREASE_ASYNC = 'INCREASE_ASYNC';
const DECREASE_ASYNC = 'DECREASE_ASYNC';

// 액션 생성 함수
export const increase = () => ({ type: INCREASE });
export const decrease = () => ({ type: DECREASE });
export const increaseAsync = () => ({ type: INCREASE_ASYNC });
export const decreaseAsync = () => ({ type: DECREASE_ASYNC });

function* increaseSaga() {
  yield delay(1000); // 1초를 기다립니다.
  yield put(increase()); // put은 특정 액션을 디스패치 해줍니다.
}
function* decreaseSaga() {
  yield delay(1000); // 1초를 기다립니다.
  yield put(decrease()); // put은 특정 액션을 디스패치 해줍니다.
}

export function* counterSaga() {
  yield takeEvery(INCREASE_ASYNC, increaseSaga); // 모든 INCREASE_ASYNC 액션을 처리
  yield takeLatest(DECREASE_ASYNC, decreaseSaga); // 가장 마지막으로 디스패치된 DECREASE_ASYNC 액션만을 처리
}

// 초깃값 (상태가 객체가 아니라 그냥 숫자여도 상관 없습니다.)
const initialState = 0;

export default function counter(state = initialState, action) {
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

2. 루트 사가 만들기

```javascript
// modules/index.js

import { combineReducers } from 'redux';
import counter, { counterSaga } from './counter';
import posts from './posts';
import { all } from 'redux-saga/effects';

const rootReducer = combineReducers({ counter, posts });
export function* rootSaga() {
  yield all([counterSaga()]);              // all 은 배열 안의 여러 사가를 동시에 실행
}

export default rootReducer;
```

3. 리덕스 스토어에 redux-saga 미들웨어 적용

```javascript
// index.js

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { createStore, applyMiddleware } from 'redux';
import { Provider } from 'react-redux';
import rootReducer, { rootSaga } from './modules';
import logger from 'redux-logger';
import { composeWithDevTools } from 'redux-devtools-extension';
import ReduxThunk from 'redux-thunk';
import { Router } from 'react-router-dom';
import { createBrowserHistory } from 'history';
import createSagaMiddleware from 'redux-saga';

const customHistory = createBrowserHistory();
const sagaMiddleware = createSagaMiddleware(); // 사가 미들웨어 생성

const store = createStore(
  rootReducer,
  composeWithDevTools(
    applyMiddleware(
      ReduxThunk.withExtraArgument({ history: customHistory }),
      sagaMiddleware, // 사가 미들웨어를 적용하고
    )
  )
); // 여러개의 미들웨어를 적용

sagaMiddleware.run(rootSaga); // 루트 사가 실행

ReactDOM.render(
  <Router history={customHistory}>
    <Provider store={store}>
      <App />
    </Provider>
  </Router>,
  document.getElementById('root')
);

serviceWorker.unregister();
```

4. App 컴포넌트에서 CounterContainer 렌더링

```javascript
// App.js

import React from 'react';
import { Route } from 'react-router-dom';
import PostListPage from './pages/PostListPage';
import PostPage from './pages/PostPage';
import CounterContainer from './containers/CounterContainer';

function App() {
  return (
    <>
      <CounterContainer />
      <Route path="/" component={PostListPage} exact={true} />
      <Route path="/:id" component={PostPage} />
    </>
  );
}

export default App;
```

