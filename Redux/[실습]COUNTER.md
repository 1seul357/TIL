```javascript
import { createStore } from "redux";

const add = document.getElementById("add");
const minus = document.getElementById("minus");
const number = document.querySelector("span");

// 초깃값
let count = 0;

number.innerText = count;

// 액션 타입
const ADD = "ADD";
const MINUS = "MINUS";

const updateText = () => {
  number.innerText = count;
// 리듀서
const countModifier = (count = 0, action) => {
  switch (action.type) {
    // action.type이 ADD 이면 count + 1
    case "ADD":
      return count + 1;
    // action.type이 MINUS 이면 count - 1
    case "MINUS":
      return count - 1;
    default:
      return count;
  }
}

// 상태 생성
const countStore = createStore(countModifier);

const onChange = () => {
  // 숫자 업데이트
  number.innerText = countStore.getState();
} 

countStore.subscribe(onChange);

const handleAdd = () => {
  // action 발생시키기
  countStore.dispatch({ type: ADD })
}

const handleMinus = () => {
  // action 발생시키기
  countStore.dispatch({ type: MINUS })
}

add.addEventListener("click", handleAdd);
minus.addEventListener("click", handleMinus);
```

