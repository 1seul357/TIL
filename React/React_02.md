# React_02

### 1) React 기초

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>      
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script> 
  <script>
    const root = document.getElementById("root");
    const span = React.createElement("span", { id: "span", style: { color: "red" }}, "Hello I'm a span" );     // span 만들고,
    const btn = React.createElement("button", null, "Click me");
    const container = React.createElement("div", null, [span, btn])
    // ReactDOM.render(span, root)
    ReactDOM.render(container, root)                 // root 안에 넣기
  </script>
</html>
```

- React는 Javascript -> html
- Javascript로 element 생성하고, React JS가 그것을 html로 번역 (ReactDOM.render( ))
- createElement( element, property, content )



```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>      
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>   
  <script>
    const root = document.getElementById("root");
    const h3 = React.createElement("h3", { onMouseEnter: () => console.log("mouse enter"), }, "Hello I'm a span");
    const btn = React.createElement("button", { onClick: () => console.log("im clicked"),}, "Click me" );
    const container = React.createElement("div", null, [span, btn])

    ReactDOM.render(container, root)
  </script>
</html>
```

- property : id, class, event listener



### 2) JSX

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    
    const Title = ( <h3 id="title" onMouseEnter ={ () => console.log("mouse enter")}> Hello I'm a title </h3> );
    const Button = <button style={{backgroundColor: "tomato"}} onClick = { () => console.log("im clicked")}> Click me </button>

    const container = React.createElement("div", null, [Title, Button])

    ReactDOM.render(container, root)      
  </script>
</html>
```

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");

    const Title = () => { return (<h3 id="title" onMouseEnter ={ () => console.log("mouse enter")}> Hello I'm a title </h3>) };
    const Button = () => <button style={{backgroundColor: "tomato"}} onClick = { () => console.log("im clicked")}> Click me </button>

    const Container = () => (
      <div>
        <Title /> 
        <Button />
      </div>
    );

    ReactDOM.render(<Container />, root)      
  </script>
</html>
```

- Javascript를 확장한 문법
- React 최종 구조
- 함수, 리턴하는 방식으로 써야 함



### 3) State

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    
    function App () {
      const [counter, setCounter] = React.useState(0);
      const onClick = () => {
        // setCounter(counter + 1);             파라미터로 전달하는 방식, 업데이트된 부분만 HTML에 반영
        setCounter((current) => current + 1);   
      }
      return (
        <div>
          <h3>Total clicks: { counter }</h3>
          <button onClick={ onClick }>Click me</button>
        </div>
      );
    }
    
    ReactDOM.render(<App />, root);
  </script>
</html>
```

- state : 컴포넌트에서 동적인 값, 상태.

- React.useState(0) : 상태의 기본값을 파라미터로 넣어서 호출. 반환되는 첫번째 원소는 현재 상태, 두번째 원소는 Setter 함수

  > useState( ) 안에 0을 넣으면 첫번째 원소인 현재 상태 값은 0
  >
  > 그러므로 counter = 0 인 상태로 렌더링

- setCounter((current) => current + 1) : 함수형 업데이트. argument의 첫번째 요소는 현재 값, 리턴되는 값은 state

  > 확실히 현재 값이라는 것을 보장, 컴포넌트 최적화할 때 사용



### 4) Input

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    function App () {
      const [minutes, setMinutes] = React.useState(0);
      const [flipped, setFlipped] = React.useState(false);
      const onChange = (event) => {
        setMinutes(event.target.value);
      };
      const reset = () => setMinutes(0);
      const onFlip = () => setFlipped((current) => !current);
      return (
        <div>
          <h1>Super Converter</h1>
          <label htmlFor="minutes">Minutes</label>
          <input value={minutes} id="minutes" placeholder="Minutes" type="number" onChange={onChange} disabled={flipped === true}/>
          <h4>You want to convert {minutes}</h4>
          <label htmlFor="hours">Hours</label>
          <input value={Math.round(minutes/60)} id="hours" placeholder="Hours" type="number" disabled={flipped === false} />
          <button onClick={reset}>Reset</button>
          <button onclick={onFlip}>Flip</button>
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
</html>
```

- label의 htmlFor와 input의 id를 같은 이름으로 설정
- input의 value 값이 변하면(onChange) onChange 함수 실행 -> setMinutes으로 minutes 값 변경 -> 실시간으로 {minutes} 변경
