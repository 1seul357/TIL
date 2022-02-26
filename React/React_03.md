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



### 2) React Practice

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

