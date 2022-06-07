# ECMA

### ECMA

- 정보 통신에 대한 표준을 제정하는 비영리 표준화 기구
- ECMA-262(범용적인 목적의 프로그래밍 언어에 대한 명세) 규격에 따라 정의한 언어

</br>
</br>

### 세미콜론

- JS는 세미콜론을 선택적으로 사용, ASI에 의해 자동으로 세미콜론이 삽입

</br>
</br>

### 변수와 식별자

식별자 : 변수를 구분할 수 있는 변수명, 반드시 문자와 달러 또는 밑줄로 시작. 대소문자 구분하며 예약어 사용 불가능

- 작성 스타일

  1. 카멜케이스 : 변수, 객체, 함수에 사용. 두번째 단어의 첫 글자부터 대문자

     ```javascript
     // 변수
     let dog
     // 객체
     const userInfo = {name: 'juan', age: 27}
     // 함수
     function getPropertyName () {}
     ```

  2. 파스칼 케이스 : 클래스와 생성자에 사용. 모든 단어의 첫번째 글자를 대문자로 작성

     ```javascript
     // 클래스
     class User {
         constructor(options) {
             this.name = options.name
         }
     }
     //생성자
     const good = new User({
         name: '홍길동',
     })
     ```

     

  3. 대문자 스네이크 케이스 : 상수에 사용, 상수(변경될 가능성이 없는 값). 모든 단어 대문자, 단어 사이에 언더스코어 삽입

     ```javascript
     //상수
     const API_KEY = 'SOMEKEY'
     ```

- 변수 선언 키워드

  - let : 재할당할 수 있는 변수 선언 시 사용, 변수 재선언 불가능, 블록스코프
  - const : 재할당할 수 없는 변수 선언 시 사용, 변수 재선언 불가능, 블록 스코프
  - var : 재선언 및 재할당 가능, 함수 스코프
    - 호이스팅 : 변수를 선언 이전에 참조, 변수 선언 이전의 위치에서 접근하면 undefined 반환

- 변수

  - 선언 : 변수를 생성
  - 할당 : 선언된 변수에 값 저장
  - 초기화 : 선언된 변수에 처음으로 값 저장

- 블록스코프 : if, for, 함수 등의 중괄호 내부

  ```javascript
  let x = 1
  if(x===1) {
      let x = 2             // 블록 스코프 안에 있는 변수는
      console.log(x)        // 2
  }
  console.log(x)            // 1, 블록 바깥에서 접근 불가능
  ```

- 함수스코프 : 함수의 중괄호 내부, 함수 바깥에서 접근 불가능

  ```javascript
  function foo() {
      var x = 5
      console.log(x)
  }
  console.log(x)
  ```

</br>
</br>

### 데이터 타입

- 원시타입 (Primitive type) : 객체가 아닌 기본 타입, 변수에 해당 타입의 값이 담김, 다른 변수에 복사할 때 실제 값 담김
  - 숫자타입 : 정수, 실수 구분 없는 하나의 숫자 타입. 부동소수점 형식. 계산 불가능한 경우 NaN 반환. 0, -0, NaN을 제외한 모든 경우 참으로 형변환
  - 문자열 타입 : 텍스트 데이터
  - undefined : 변수의 값이 없음. 변수 선언 이후 값 할당하지 않으면 자동으로 할당. typeof = undefined
  - null : 변수의 값이 없음을 의도적으로 표현. typeof = null
  - Boolean : 논리적 참 또는 거짓 표현. true 또는 false
- 참조타입 (Reference type) : 객체 타입의 자료형, 변수에 해당 객체의 참조 값이 담김, 다른 변수에 복사할 때 참조 값 복사
  - 함수, 배열, 객체

</br>
</br>

### 연산자

- 할당 연산자
- 비교 연산자 :  <,  > 등등 결과값을 boolean으로 반환
- 동등 비교 연산자 : == 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교
- 일치 비교 연산자 : === 압묵적 타입 변환 발생하지 않음. 엄격한 비교(두 비교 대상의 타입과 값이 모두 같은지 비교)를 통해 boolean 값 반환
- 논리 연산자 : &&, ||, !
- 삼항 연산자 : 세개의 피연산자를 사용하여 조건에 따라 값 반환

</br>
</br>

### 조건문

- if : 조건 표현식의 결과값을 Boolean 타입으로 변환 후 참 / 거짓 판단

  ```javascript
  const username = 'admin'
  
  if (username=='admin') {
    console.log('관리자님 환영합니다')
  }
  else if (username=='manager') {
    console.log('매니저님 환영합니다.')
  }
  else {
    console.log(` ${username}님 환영합니다.`)
  }
  ```

- switch : 조건 표현식의 결과값이 어느 값(case)에 해당하는지 판별. 조건 분기

  ```javascript
  const operator = '+'
  const numOne = 1
  const numTwo = 10
  
  switch (operator) {
    case '+': {
      console.log(numOne + numTwo)
      break
    }
    case '-': {
      console.log(numOne - numTwo)
      break
    }
    case '*': {
      console.log(numOne * numTwo)
      break
    }
    case '/': {
      console.log(numOne / numTwo)
      break
    }
    default: {
      console.log('유효하지 않은 연산자입니다.')
    }
  }
  ```

  - break 문이 없는 경우 break문을 만나거나 default문을 실행할 때까지 다음 조건문 실행

</br>
</br>

### 반복문

- while : 조건문이 참인 동안 반복

  ```javascript
  while (condition) {
      // 실행할 코드
  }
  ```

- for

  ```javascript
  for (initialization; condition; expresion) {
      // initialization : 최초 반복문 진입 시 1회만 실행
      // condition : 매 반복 시행 전 평가되는 부분
      // expression : 매 반복 시행 이후 평가되는 부분
  }
  
  for (let i = 0; i < 6; i++) {
      console.log(i)
  }
  ```

- for ... in : 객체의 속성들을 순회할 때 사용

  ```javascript
  const capitals = {
      Korea: '서울',
      France: '파리',
      USA: '미국'
  }
  
  for (let capital in capitals) {
      console.log(capital)    // Korea, France, USA
  }
  ```

- for ... of : 반복 가능한 객체를 순회(배열 원소 순회)하며 값을 꺼낼 때 사용 (Array, Map, Set, String)

  ```javascript
  const fruits = ['딸기', '바나나', '메론']
  
  for (let fruit of fruits) {
      console.log(fruit)
  }
  ```

</br>
</br>

### 함수

- 함수

  - 함수 선언식 : 익명 함수 불가능, 호이스팅 O (함수 호출 이후에 선언해도 동작, var 키워드로 함수 표현식 작성하면 에러 발생)
  - 함수 표현식 : 익명 함수 가능, 호이스팅 X (함수 호출 이후에 선언하면 에러 발생)

  ```javascript
  // 함수 선언식
  function name(args) {
      return num
  }
  
  // 함수 표현식
  const add = function (numOne, numTwo) {
      return numOne + numTwo
  }
  
  const greeting = function (name = 'noName') {
      console.log(`hi ${name}`)
  }
  greeting()
  ```

- 자바스크립트의 함수는 일급 객체

  - 일급 객체 : 변수에 할당 가능, 함수의 매개변수로 전달 가능, 함수의 반환 값으로 사용 가능

- Arrow Function : 화살표 함수

  - function 키워드 생략 가능, 매개변수가 한개이면 () 도 생략 가능. 몸통이 표현식 하나라면 {}과 return도 생략 가능

  ```javascript
  const arrow = function (name) {
      return `hello ${name}`
  }
  
  const arrow = (name) => {
      return `hello ${name}`
  }
  
  const arrow = name => {
      return `hello ${name}`
  }
  
  const arrow = name => `hello ${name}`
  ```

</br>
</br>

### 배열

- 키와 속성들을 담고 있는 참조 타입의 객체
- 양의 정수 인덱스로 특정 값에 접근, array[-1]로 접근 X
- array.length로 접근 가능. array.length-1, array.length-2...

| **reverse**         | **원본 배열의 요소들의 순서를 반대로 정렬**         |
| ------------------- | --------------------------------------------------- |
| **push & pop**      | **배열의 가장 뒤에 있는 요소를 추가 또는 제거**     |
| **unshift & shift** | **배열의 가장 앞에 요소를 추가 또는 제거**          |
| **includes**        | **배열에 특정 값이 있는지 판별 후 참 / 거짓 반환**  |
| **indexOf**         | **배열에 특정 값이 존재하는지 판별 후 인덱스 반환** |
| **join**            | **배열의 모든 요소를 구분자를 이용하여 연결**       |

```javascript
const numbers = [1, 2, 3, 4, 5]
numbers.reverse()   // [5, 4, 3, 2, 1]
numbers.push(100)   // [1, 2, 3, 4, 5, 100]
numbers.pop()       // [1, 2, 3, 4, 5]
numbers.unshift (100)   // [100, 1, 2, 3, 4, 5]
numbers.shift()       // [1, 2, 3, 4, 5]
console.log(numbers.includes(1))   // true
numbers.indexOf(3)   // 2. 가장 첫 번째로 찾은 요소의 "인덱스" 반환
numbers.join('-')   // 1-2-3-4-5
```

1. forEach : 배열의 각 요소에 대해 콜백 함수를 한번씩 실행. 반환 값이 없는 메서드

   ```javascript
   forEach(element, index, array)   // 배열의 요소, 인덱스, 배열
   
   const ssafy = ['광주', '서울', '구미', '대전', '부울경']
   
   ssafy.forEach(region, index) => {
       console.log(region, index)    // 광주 0, 서울 1 
   }
   ```

2. map : 콜백 함수의 반환 값을 요소로 하는 새로운 배열 반환

   ```javascript
   const numbers = [1, 2, 3, 4, 5]
   const doubleNums = numbers.map((num) => {
       return num*2
   })
   console.log(doubleNums)  // [2, 4, 6, 8, 10]
   ```

3. filter : 콜백 함수의 반환 값이 참인 요소들만 모아서 새로운 배열 반환

   ```javascript
   const numbers = [1, 2, 3, 4, 5]
   const oddNums = numbers.filter((num, index) => {
       return num%2    // 1, 3, 5
   })
   ```

4. reduce : 콜백 함수의 반환 값들을 하나의 값(acc)에 누적 후 반환

   ```javascript
   const numbers = [1, 2, 3]
   const result = numbers.reduce((acc, num) => {
       return acc + num
   }, 0)   // 0 : initialValue : 최초 콜백 함수 호출 시 acc에 할당되는 값
   ```

5. find : 콜백 함수의 반환 값이 참이면 해당 요소 반환

   ```javascript
   const accounts = [
   	{ name: 'justin', balance: 1200 },
   	{ name: 'harry', balance: 50000 },
   	{ name: 'jason', balance: 24000 },
   ]
   
   const result = accounts.find(function (account) {
     return account.balance === 24000   // { name: 'jason', balance: 24000 }
   })
   ```

6. some : 배열의 요소 중 하나라도 주어진 판별 함수를 통과하면 참 반환, 모든 요소가 통과하지 못하거나 빈 배열은 거짓 반환

   ```javascript
   const requests = [
     { url: '/photos', status: 'complete' },
     { url: '/albums', status: 'pending' },
     { url: '/users', status: 'failed' },
   ]
   
   const result = requests.some(function (request) {
     return request.status === 'pending'   // true
   })
   ```

7. every : 배열의 모든 요소가 주어진 판별 함수를 통과하면 참 반환

   ```javascript
   const users = [
     { name: 'Harry', submitted: true },
     { name: 'Eric', submitted: true },
     { name: 'Tony', submitted: false },
   ]
   
   const result = users.every(user => {
     return user.submitted === true    // false
   })
   ```

</br>
</br>

### 객체

- 속성의 집합. key와 value로 표현
- key는 문자열 타입만 가능, value는 모든 타입 가능

```javascript
const data = {
  id: 42,
  items: [
    {
      id: 1,
      name: 'foo',
    },
    {
      id: 2,
      name: 'bar',
    },
  ],
}

const result = data.items[0].name   // 속성에는 ., []를 통해 접근 가능
console.log(result)
```

- 속성명 축약 : 객체 정의할 때, key와 할당하는 변수의 이름 같으면 축약 가능

```javascript
const user = {
  username: username,
  contact: contact,
}

const user = {
  username,
  contact,
}
```

- 메서드명 축약 : function 키워드 생략 가능

- 계산된 속성 : 객체를 정의할 때 key 이름을 표현식을 이용하여 동적으로 생성 가능

```javascript
const key = 'regions'
const value = ['광주', ' 대전', '구미', '서울']

const ssafy = {
    [key]: value,
}

console.log(ssafy.regions)  // ['광주', '대전', '구미', '서울']
```

- 구조분해 할당 : 배열 또는 객체를 분해하여 속성을 변수에 쉽게 할당할 수 있는 문법

```javascript
const users = [
  {
    name: 'hailey',
    contact: '010-1234-5678',
  },
  {
    name: 'paul',
    contact: '010-5678-1234',
  },
]

function saveUserData (users) {
  const userData = users.map(({name, contact} , index) => {
    return { 
      id: index, 
      name,
      contact,
    }
  })
  return userData
}

saveUserData(users)
```

- JSON : key-value 쌍의 형태로 데이터를 표기하는 언어 독립적 표준 포맷
  - JSON.parse() : JSON -> 자바스크립트 객체
  - JSON.stringify() : 자바스크립트 객체 -> JSON
