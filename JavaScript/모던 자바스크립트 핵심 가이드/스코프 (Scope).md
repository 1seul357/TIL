# 스코프 (Scope)

ES5까지 변수를 선언하기 위해서는 var 키워드를 사용해야 했고, 따라서 함수 외부에서 생성한 변수는 모두 전역 변수가 되었다. 이는 호이스팅, 변수 중복 선언, 코드의 복잡성 등 여러가지 문제를 일으키는 원인이 된다. var의 단점을 해결하기 위해 let과 const가 도입되었다.

</br>

</br>

### 스코프

- 스코프는 '범위'를 의미하며 자바스크립트에서도 '범위'를 의미한다.
- 식별자 접근 규칙에 따른 유효범위이다.
- 식별자 (변수, 함수, 클래스)에 접근할 수 있는 범위가 존재한다.
- 스코프는 블록 또는 함수에 의해 나눠진다.

</br>

</br>

### 블록 레벨 스코프와 함수 레벨 스코프

**함수 레벨 스코프 (Function-level scope)** : 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 함수 내부에서 선언된 변수 = 지역변수, 함수 외부에서 선언된 변수 = 전역변수

**블록 레벨 스코프 (Block-level scope)** : 모든 코드 블록 (함수, for문, while문 등) 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다. 코드 블록 내부에서 선언된 변수 = 지역변수

</br>

</br>

### var 키워드

var는 함수 스코프이며, 재선언 및 재할당이 가능하다. 또한 호이스팅도 가능하다. var는 초기값이 없으면 자동으로 메모리를 할당하므로 에러가 발생하지 않는다.

```javascript
for (var i = 0; i < 10; i++) {
	var leak = "I am available outside of the loop";
}

console.log(leak);

function myFunc() {
	var functionScoped = "I am available inside this function";
	console.log(functionScoped);
}

myFunc();
console.log(functionScoped);
```

var 키워드로 선언한 변수는 오직 함수의 코드 블록만을 지역 스코프로 인정한다. 함수 외부에서 var 키워드로 선언한 변수는 코드 블록 내에서 선언해도 모두 전역 변수가 된다.

변수 leak는 함수 외부에서 선언했으므로 전역 변수이다. 그래서 console.log()로 출력해도 값이 오류 없이 출력된다.

하지만 변수 functionScoped는 함수 내부에서 선언했으므로 지역 스코프이다. console.log()로 값을 출력하면 오류가 발생한다.

</br>

</br>

### let 키워드

블록 스코프이므로 변수가 선언된 블록과 그 하위 블록 내에서만 사용할 수 있다. let 키워드로 선언한 변수는 값을 재할당할 수 있지만 재선언은 불가능하다.

```javascript
for (let i = 0; i < 10; i++) {
	console.log(i);
}

console.log(i); // Error
```

블록 스코프 안에서 let으로 선언한 변수는 스코프 안에서만 참조 가능하다. 그러므로 i를 블록 밖에서 출력하려고 하면 에러가 발생한다.

```javascript
let x = "global";

if (x === "global") {
    let x = "block-scoped";
    console.log(x); // block-scoped
}

console.log(x); // global
```

x는 블록이 다르므로 재선언이 아닌 서로 다른 변수이다. 그러므로 오류가 발생하지 않는다.

```javascript
// 재할당 가능
let x = "global";
x = "block";

// 재선언 불가능
let x = "global";
let x = "block";
```

</br>

</br>

### const 키워드

블록 스코프이며 재할당과 재선언 모두 불가능하다. const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.

```javascript
// 재할당 불가능
const constant = "I am a constant";
constant = "I can't be reassigned";

const person = {
	name: 'Alberto',
	age: 25,
};

person.age = 26;
console.log(person.age); // 26
```

const 는 변수의 속성 중 일부만 재할당하는 것은 가능하다. 즉 원시 값은 불가능하지만 객체는 된다는 것이다. 위의 코드는 변수 전체 재할당이 아닌 변수의 속성 중 하나만 재할당하는 것이므로 오류가 발생하지 않는다.

</br>

</br>

### const를 사용하자!

var는 유효범위가 넓기 때문에 가급적이면 var를 사용하지 않아야 한다. 변수 선언 시에는 기본적으로 const를 사용하고, let은 재할당이 필요한 경우에 한정하여 사용하는 것이 좋다. const 키워드를 사용하면 의도치 않은 재할당을 방지해 주기 때문에 웹 프로그래밍 시 안전하다. 또한 오류를 줄이기 위해서는 변수의 스코프는 최대한 좁게 만드는 것이 좋다.

- var는 함수의 코드 블록만을 스코프로 인정한다. 따라서 함수 외부에서 생성한 변수는 모두 전역 변수이다. 전역 변수를 남발할 가능성이 있기 때문에 사용하지 않는 것이 좋다.
- 의도하지 않은 변수 값의 변경 (재선언, 재할당)이 발생할 수 있다.
- var는 호이스팅이 가능하므로 변수를 선언하기 전에 참조할 수 있다.