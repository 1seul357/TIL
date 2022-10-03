# Typescript_01

### 📑 Typescript

타입스크립트는 자바스크립트에 타입을 부여한 언어이다. 자바스크립트의 확장된 언어라고 볼 수 있으며 브라우저에서 실행하기 위해 파일을 한번 변환해주어야 한다. 이러한 과정을 컴파일이라고 한다.

</br>
</br>

### 특징

- 컴파일 언어이며 정적 타입 언어이다.

  > 자바스크립트는 동적 타입의 인터프리터 언어로 런타임에서 오류를 발견할 수 있다. 하지만 타입스크립트는 정적 타입의 컴파일 언어로 컴파일러 또는 바벨을 통해 자바스크립트 코드로 변환된다. 코드 작성 단계에서 타입을 체크해 오류를 확인할 수 있고 미리 타입을 결정하기 때문에 실행 속도가 매우 빠르다.

- 자바스크립트 슈퍼셋이다.

  > 자바스크립트로 작성한 코드는 확장자를 .ts로 변경하고 타입스크립트로 컴파일해 변환할 수 있다.

- 객체 지향 프로그래밍을 지원한다.

  > 타입스크립트는 ES6에서 새롭게 사용된 문법을 포함하고 있으며 클래스, 인터페이스, 상속, 모듈 등과 같은 객체 지향 프로그래밍 패턴을 제공한다.

</br>
</br>

### Typescript를 쓰는 이유

- 높은 수준의 코드 탐색과 디버깅

  > 코드에 목적을 명시하고 맞지 않는 타입의 변수나 함수들에서 에러를 발생시켜 오류를 사전에 제거할 수 있다. 또한 코드 자동완성을 통해 작업과 동시에 디버깅이 가능해 생산성을 높일 수 있다.

- 자바스크립트 호환

  > 타입스크립트는 자바스크립트와 호환된다. 앱과 웹을 구현하는 자바스크립트와 동일한 용도로 사용할 수 있다.

- 라이브러리

  > 대부분의 라이브러리들이 타입스크립트를 지원하며 VSCode에서도 타입스크립트 관련 기능과 플러그인을 지원한다.

</br>
</br>

### 변수와 함수 타입

- 기본 타입

  ```typescript
  // 문자열
  var str: string = 'hello';
  
  // 숫자
  let num: number = 10;
  
  // 배열
  let arr: Array<number> = [1, 2, 3];
  let items: number[] = [1, 2, 3];
  let arr2: Array<String> = ['Capt', 'Thor', 'Hulk'];
  
  // 튜플
  let address: [string, number] = ['abc', 100];
  
  // 객체
  let obj:object = {};
  let person: object = {
      name: 'capt',
      age: 100
  };
  let person: { name:string, age:number } = {
      name: 'thor',
      age: 1000
  }
  
  // 진위값
  let show: boolean = true;
  ```

- 함수 타입

  ```typescript
  // 함수의 파라미터에 타입을 정의하는 방식
  function sum(a: number, b: number) {
      return a+b;
  }
  sum(10, 20);
  
  // 함수의 반환 값에 타입을 정의하는 방식
  function add(): number {
      return 10;
  }
  
  // 함수에 타입을 정의하는 방식 (가장 기본적인 방식)
  function sum(a: number, b: number): number {
      return a+b;
  }
  
  // 함수의 옵셔털 파라미터
  function log(a: string, b?: string, c?: string) {    // a는 필수, b는 선택
      
  }
  log('hello world', 100);
  ```

</br>
</br>

### void와 any

- `void` : 리턴 값이 없음

- `any` : 어떤 형식이든 상관 없음

</br>
</br>

### filter와 화살표 함수

```typescript
let arr = [
    { gender: 'male', name: 'john' },
    { gender: 'female', name: 'sarah' },
    { gender: 'male', name: 'bone'},
]

const filtered arr.filter(function(item) {
    if (item.gender === 'female') {
        return item;
    }
})

console.log(filtered);


function addTodoItems() {
    const item1 = {
        id: 4,
        title: '아이템 4',
        done: false,
    }
    addTodo(item1);
}
```

</br>
</br>

### 인터페이스

인터페이스는 상호 간에 정의한 약속 혹은 규칙을 의미한다.

- 객체의 스펙 (속성과 속성의 타입)
- 함수의 파라미터
- 함수의 스펙 (파라미터, 반환 타입)
- 배열과 객체를 접근하는 방식
- 클래스

```typescript
// 인터페이스 정의
interface User {
    age: number;
    name: string;
}

// 변수에 인터페이스 활용
var seho: User = {
    age: 33,
    name: '세호'
}

// 함수에 인터페이스 활용
function getUser(user: User) {
    console.log(user);
}
const capt = {
    age: 10,
    name: '캡틴',
}
getUser(capt);

// 함수의 구조에 인터페이스 활용
interface SumFunction {
    (a: number, b: number): number;
}

let sum: SumFunction;
sum = function(a: number, b: number): number {
    return a + b;
}
```

</br>
</br>

### 타입 별칭

타입 별칭은 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수를 의미한다. 새로운 타입 값을 생성하는 것이 아니라 정의한 타입에 대해 쉽게 참고할 수 있게 이름을 부여하는 것이다. 인터페이스와는 프리뷰에 있어서 차이가 있다.

```typescript
// string 타입 사용
const name: string = 'capt';

// 타입 별칭 사용
type MyName = string;
const name: myName = 'capt';
```

