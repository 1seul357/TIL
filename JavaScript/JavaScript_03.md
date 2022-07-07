# JavaScript

### AJAX

브라우저에서 페이지 이동 없이 자바스크립트를 통해 HTTP REQUEST를 보내고, 그 응답을 받아서 처리할 수 있는 기능이다.

- 상호 작용성이 향상

- 서버에 대한 요청 감소

- 동적 페이지 북마크가 어려움

</br>

</br>

### JSON

자바스크립트 객체를 문자열로 표현이다. 서버 -> 브라우저로 정보를 보낼 때, JSON 파일로 보내고 브라우저는 이를 자바스크립트로 파싱한다.

</br>

</br>

### SCOPE

var : function 단위 스코프 변수이며 재선언 및 재할당이 가능하다.

> var는 함수 내부에 선언된 변수만 지역변수로 한정하며, 나머지는 모두 전역변수로 간주한다. 

```javascript
function test() {
    var a = 10
    console.log(a)          // 10
    
    if(true) {
        var a = 20                             // 재선언 가능
        console.log(a)      // 20
    }
    
    console.log(a)          // 20
}
```

```javascript
funciont test() {
    var choco = "초코";          // 지역변수
    console.log(choco)          // 초코
}

test();

console.log(choco);            // 오류 발생

if(true) {
    var choco = "초코"              // 전역변수
    console.log(choco);            // 초코
}

console.log(choco);             // 초코
```

const : 블록 단위 스코프 변수이며 재선언 및 재할당이 불가능하다.

```javascript
function test() {
    const num = 10
    const num = 555         // 재선언 불가능
    
    console.log(num)        // 오류 발생
}
```

```javascript
// 블록 단위 스코프 변수이므로 블록 밖에서 변수를 출력하면 오류 발생

if(true) {
    var choco = "초코"              // 전역변수
    console.log(choco);            // 초코
}

console.log(choco);             // 오류 발생
```

let : 블록 단위 스코프 변수이며 재할당만 가능하다.

```javascript
function test() {
    let num = 10
    num = 555                // 재할당 가능
    
    console.log(num)
}

function test() {
    let num = 10
    let num = 555            // 재선언 불가능
    
    console.log(num)         
}
```

```javascript
// 블록 단위 스코프 변수이므로 블록 밖에서 변수를 출력하면 오류 발생

if(true) {
    var choco = "초코"              // 전역변수
    console.log(choco);            // 초코
}

console.log(choco);             // 오류 발생
```

</br>

</br>

### 동기함수와 비동기함수

동기함수 : 블로킹, 명령문이 순서대로 진행된다.

비동기함수 : 요청과 응답의 결합이 비동기적이라 실행 결과를 기다리지 않아도 된다.

</br>

</br>

### 호스트 객체와 네이티브 객체

호스트 객체 : 빌트인 또는 네이티브 객체에 포함되지 않은 사용자에 의해 생성된 객체이다.

- 전역 객체, BOM 등
- window, XmlHttpRequest, HTMLElement 등의 DOM 노드 객체와 같이 호스트 환경에 정의된 객체

네이티브 객체 : 자바스크립트 언어 규약(ECMAScript)으로 정의되어진 객체이다. 애플리케이션 전역의 공통 기능을 제공한다. 네이티브 객체는 애플리케이션의 환경과 관계없이 언제나 사용할 수 있다.

- 모든 built-in object(내장 객체)를 포함한다.
- Null, undefined, Function, Number, Math 등

</br>

</br>

### undeclared

undeclared : var, const 등을 사용하여 생성되지 않은 식별자에 값을 할당할 때 나타난다.

undefined : 변수는 생성되었으나 값이 할당되지 않은 것이다.

null : null 값이 명시적으로 할당된다.

</br>

</br>

### this **객체**

함수를 호출하는 객체에 대한 참조이다. this는 어떻게 호출되었느냐에 따라 결정된다.

**전역에서의 this** : window 객체

**일반 함수의 this** : window

**객체 메서드의 this** : 함수를 어떤 객체의 메소드로 호출하면 this의 값은 그 객체를 사용한다.

```javascript
var o = {
    prop: 37,
    f: function() {
        return this.prop()
    }
}

console.log(o.f());     // 37
```

</br>

</br>

### 호이스팅

스코프를 정의할 때 순서와 상관없이 선언부(선언 O, 할당 X)에 대한 해석 처리를 최우선시 하는 것이다. 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언한다. 즉 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.

- 자바스크립트 Parser가 함수 실행 전에 해당 함수를 훑는다.
- 함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킨다.
- 유효 범위 : 함수 블록 `{}` 안에서 유효
- var를 사용한 선언문에서는 호이스팅이 일어나지만 let, const, class는 호이스팅이 발생하지 않는 것처럼 동작한다.

</br>

</br>

### 클로저

함수와 함수가 선언된 어휘적(lexical) 환경의 조합. 클로저는 어떤 함수가 자신의 내부가 아닌 외부에서 선언된 변수에 접근하는 것이다. 

- 내부 함수에서는 외부 함수 스코프에서 선언된 변수에 접근 가능하다.

- 함수가 호출되는 환경과 별개로, 기존에 선언되어 있던 환경(어휘적 환경)을 기준으로 변수를 조회한다.

  > 외부함수의 실행이 종료되어도, 클로저 함수는 외부함수의 스코프, 즉 함수가 선언된 어휘적 환경에 접근할 수 있다.

사용하는 이유

- 상태 유지 : 현재 상태를 기억하고, 변경된 최신 상태를 유지할 수 있다.

- 전역 변수의 사용 억제 : 상태 변경이나 가변 데이터, 오류를 피하고, 안정성을 증가시킬 수 있다.

- 정보 은닉 : 클래스 기반 언어의 private 키워드처럼 사용할 수 있다.

```javascript
function outter() {
    var title = 'closer';
    return function() {
        alert(title);
    }
}

inner = outter();       
inner();                  // closer 출력
```

outter 함수가 종료되면 외부함수의 지역변수 title은 소멸되어야 하지만 innter() 함수 호출 시 closer가 출력된다. 이는 내부함수가 외부함수의 지역변수에 접근하고, 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성때문이다.