```javascript
import { createStore } from "redux";

const form = document.querySelector("form");
const input = document.querySelector("input");
const ul = document.querySelector("ul");

// 액션 타입 생성
const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";

// 오브젝트 형식으로 return 하기 위해 사용
const addToDo = (text) => {
  return {
    type: ADD_TODO,
    text
  }
}

const deleteTodo = id => {
  return {
    type: DELETE_TODO,
    id
  }
}

// 리듀서 생성
const reducer = (state = [], action) => {
  switch(action.type) {
    case ADD_TODO:
          // 리스트에 추가하면서 이전 목록 복사
      return [ { text: action.text, id: Date.now() }, ...state];
    case DELETE_TODO:
          // 리스트에서 삭제
      return state.filter(toDo => toDo.id !== action.id);
    default:
      return state;
  }
}

// store 생성
const store = createStore(reducer);

store.subscribe(() => console.log(store.getState()));

// JS 업데이트
const paintTodos = () => {
  const toDos = store.getState();
  ul.innerHTML = "";
  toDos.forEach(toDo => {
    const li = document.createElement("li");
    const btn = document.createElement("button");
    btn.innerText = "DEL";
    btn.addEventListener("click", dispatchDeleteToDo);
    li.id = toDo.id
    li.innerText = toDo.text;
    li.appendChild(btn);
    ul.appendChild(li);
  })
}

store.subscribe(paintTodos)

// dispatch 통해 액션 호출
const dispatchAddTodo = text => {
  store.dispatch(addToDo(text))
};

// dispatch 통해 액션 호출
const dispatchDeleteToDo = e => {
  const id = parseInt(e.target.parentNode.id);
  store.dispatch(deleteTodo(id));
}

const onSubmit = e => {
  e.preventDefault();
  const toDo = input.value;
  input.value = "";
  dispatchAddTodo(toDo);
};

form.addEventListener("submit", onSubmit);
```

