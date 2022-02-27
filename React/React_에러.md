# React 에러

#### 1) `React.jsx: type is invalid -- expected a string (for built-in components) or a class/function (for~)`

원인 : `export default App () ;`

해결 방법 : `export default App;`

알게된 점 : 해당 오류는 대부분 import를 잘못 하거나, 경로 오류, 대소문자를 잘못 쓴 경우에 발생

