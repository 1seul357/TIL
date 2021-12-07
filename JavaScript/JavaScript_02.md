# JavaScript

##### AJAX

- Asynchronous JavaScript And XML (비동기식 JavaScript와 XML)

- 서버와 통신하기 위해 XMLHttpRequest 객체 활용

  - XMLHttpRequest : 서버와 상호작용하기 위해 사용되며 전체 페이지 새로고침 없이 데이터 받을 수 있음,

    모든 종류의 데이터 받아올 수 있음

- JSON, XML, HTML 등 다양한 포맷 주고 받을 수 있음

- 페이지를 새로고침하지 않고서도 수행되는 비동기성(일부분만 업데이트)

##### Asynchronous JavaScript

- 동기식(Synchronous) : 순차적, 직렬적 Task 수행. 요청을 보낸 후 응답을 받아야만 다음 동작이 이루어짐

- 비동기식(Asynchronous) : 병렬적 Task 수행. 요청을 보낸 후 응답을 기다리지 않고 다음 동작 이루어짐(non-blocking)

- 비동기를 사용하는 이유 : "사용자 경험" 데이터를 요청하고 응답받는 동안, 앱 실행을 함께 진행하여 유연한 사용자 경험 제공

- Threads : 프로그램이 작업을 완료하기 위해 사용할 수 있는 단일 프로세스. 하나의 스레드는 한 번에 하나의 작업만 수행할 수 있음. 자바스크립트는 단일 스레드!

- 자바스크립트의 작업 수행 과정
  1. 즉시 처리하지 못하는 이벤트들을 Web API에 줄을 세우고,
  2. 처리된 이벤트들은 처리된 순서대로 Task queue에 넣고,
  3. Casll Stack이 비면 Event Loop가 대기 줄에서 가장 오래된 이벤트를 Call Stack으로 보냄(FIFO)
  
- Concurrency model

  > Call Stack : 요청이 들어올 때마다 해당 요청을 순차적으로 처리하는 Stack(LIFO) 형태의 자료구조
  >
  > Web API : 브라우저 영역에서 제공하는 API. 시간이 소요되는 일들을 여기서 처리
  >
  > Task Queue : 비동기 처리된 callback 함수가 대기하는 Queue(FIFO)
  >
  > Event Loop : Call Stack이 비어있는지 확인하고 Task Queue에서 실행대기 중인 callback 함수가 있는지 확인하여 callback함수를 Call Stack으로 push

- Zero delays : JavaScript가 요청을 처리하는데 필요한 최소 시간. setTimeout 함수에 특정 시간제한을 설정하면 대기중인 메시지의 모든 코드가 완료될때까지 대기해야 함

- 순차적인 비동기 처리 : Async callbacks, promise-style

##### Callback function

- 다른 함수에 인자로 전달된 함수

- 동기식, 비동기식 모두 사용

- JS의 함수는 일급 객체

  > 일급 객체 : 다른 객체들에 적용할 수 있는 연산을 모두 지원하는 객체
  >
  > 일급 객체 조건 : 인자로 넘길 수 있고, 변수에 할당할 수 있고, 함수의 반환 값으로 사용 가능해야 함

- Async callbacks : 백그라운드에서 코드 실행을 시작할 함수를 호출할 때 인자로 지정된 함수. 백그라운드 코드 실행이 끝나면 callback 함수를 호출하여 작업이 완료되었음을 알리거나, 다음 작업을 실행하게 할 수 있음

- callback function 사용하는 이유 : 다른 함수의 매개변수로 전달하여 해당 함수 내에서 특정 시점에 호출할 수 있다,

- callback Hell : 여러 개의 연쇄 비동기 작업할 때 발생 -> Promise 콜백 방식 사용

##### Promise

- 비동기 작업의 최종 완료 또는 실패를 나타내는 객체

  ```html
  <script>
      const URL = 'https://jsonplaceholder.typicode.com/todos/1/'
  
      axios.get(URL)
        .then(response => {
          return response.data
        })
        .then(response => {
          return response.title
        })
        .then(response => {
          console.log(response)
        })
        .catch(error => {
          console.log(error)
        })
        .finally(function () {
          console.log('나는 무조건 실행')
        })
    </script>
  ```
  
- Promise methods

  - .then(callback) : 이전 작업이 성공했을 때 수행할 작업을 나타내는 callback 함수, 각 callback 함수는 이전 작업의 성공 결과를 인자로 전달받음
  - .catch(callback) : .then이 하나라도 실패하면 동작
  - 각각의 .then()블록은 서로 다른 promise를 반환하기 때문에 여러 비동기 작업을 차례대로 수행할 수 있음
  - 반환 값 반드시 있어야 함
  - .finally(callback) : Promise 객체를 반환, 무조건 callback 함수 실행, 전달받는 인자 없음

- Promise 특징

  1. callback 함수는 Event Loop가 현재 실행 중인 Call Stack을 완료하기 이전에는 절대 호출되지 않음
  2. .then()을 여러번 사용하여 여러 개의 callback 함수 추가 가능(Chaining)

##### Axios

- 브라우저를 위한 Promis 기반의 클라이언트

- 편리한 AJAX 요청 가능하게 함


##### async & await

- 비동기 코드를 작성하는 방법, Promise 구조의 then chaining을 제거
- Syntactic sugar : 더 쉽게 읽고 표현할 수 있도록 설계된 프로그래밍 언어 내의 구문

