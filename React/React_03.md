# React_03

### 1) Props

```react
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    function Btn(props) {
      console.log(props);
      return (
        <button
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
          }}
        >
        { props.text }
        </button>
      )
    }
    function App () {
      return (
        <div>
          <Btn text="Save Changes" />
          <Btn text="Continue" />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
</html>
```

- props : properties. 어떠한 값을 컴포넌트에 전달할 때 사용

  

```react
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    function Btn({ text, changeValue }) {      // changeValue = prop
      return (
        <button
          onClick={changeValue}  // onClick = eventListener, 버튼 클릭 시 changeValue 실행
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
          }}
        >
        { text }
        </button>
      )
    }
    function App () {
      const [value, setValue] = React.useState("Save Changes");
      // button의 value를 Revert Changes로 변경
      const changeValue = () => setValue("Revert Changes"); 
      return (
        <div>
          <Btn text={value} changeValue={changeValue} />
          <Btn text="Continue" />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
</html>
```

- App 안에 있는 Btn(컴포넌트)의 요소들은 모두 prop

  > style이나 이벤트 리스너 등 사용 불가

- props 장점 : 반복되는 구조를 컴포넌트로 지정해서 재사용할 수 있음



### 2) useEffect

```react
import { useEffect, useState } from "react";

function App() {
  const [counter, setValue] = useState(0);
  const [keyword, setKeyword] = useState("");
  const onClick = () => setValue((prev) => prev + 1)
  const onChange = (event) => setKeyword(event.target.value);
  console.log("i run all the time.")
  useEffect(() => {
    console.log("CLASS THE API...");       // 페이지가 마운트 되었을 때, 한번 실행
  }, []);                              // deps가 빈 배열이므로
  useEffect(() => {
    // keyword가 null 값이 아니고, 길이가 5 이상이면 실행
    if (keyword !== "" && keyword.length > 5) {    
      console.log("SEARCH FOR", keyword);
    }
  }, [keyword]);                       // deps는 [keyword]

  return (
    <div>
          <!--value값에 변화가 있으면 onChage 함수 실행-->
      <input value={keyword} onChange={onChange} type="text" placeholder="Search here..."/>
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  )
}

export default App;
```

- useEffect : 컴포넌트가 마운트되었을 때, 언마운트 되었을 때, 업데이트 되었을 때 특정 작업 처리

  >  첫 번째 파라미터에는 함수, 두 번째 파라미터에는 deps

- deps : 특정 값이 들어가면 컴포넌트가 처음 마운트 될 때에도 호출, 지정한 값이 바뀔 때에도 호출, 언마운트 시에도 호출

  > deps가 빈 값이라면 컴포넌트가 처음 나타날때에만 useEffect 함수 호출

  

```react
import { useEffect, useState } from "react";

function Hello () {
  useEffect(() => {
    console.log('Im here!')
  }, []);
  return <h1>Hello</h1>;              // celanup 함수
}

function App () {
  const [showing, setShowing] = useState(false);
  const onClick = () => setShowing((prev) => !prev);
  return <div>
      {showing ? <Hello /> : null}
      <button onClick={onClick}>{showing ? "Hide" : "Show"}</button>
    </div>;
}

export default App;
```

- cleanup : useEffect에서 함수 반환 시 이를 cleanup 함수라고 함, deps가 비어있는 경우에는 컴포넌트가 사라질 때 cleanup 함수 호출

  

### 3) React Practice

`npx create-react-app react-for-beginners`

`npm start`

`npm i prop-types`

```javascript
// Button.js (자식 컴포넌트)


import PropTypes from "prop-types";
import styles from "./Button.module.css";

function Button({text}){
  return <button className={styles.btn}>{text}</button>;
}

Button.propTypes = {
  text: PropTypes.string.isRequired,
}

export default Button;
```

- propTypes : 부모로부터 전달받은 prop의 데이터 type을 검사함

  > 자식 컴포넌트에서 명시해 놓은 데이터 타입과 부모로부터 넘겨받은 데이터 타입이 일치하지 않으면 에러 발생

- App.js(부모)의 Button prop은 text = { "Continue" } 이므로 string이다. 

- Button.module.css에서 button을 스타일링하고, import해서 style에 적용



```css
// Button.module.css


.btn {
  color: white;
  background-color: tomato;
}
```

```javascript
// App.js (부모 컴포넌트)


import Button from "./Button";
import styles from "./App.module.css";

function App() {
  return (
    <div>
      <h1 className={styles.title}>Welcome back!!!</h1>
      <Button text={"Continue"} />
    </div>
  )
}

export default App;
```

