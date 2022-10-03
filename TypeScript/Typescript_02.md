# Typescript_02

### 연산자를 이용한 타입 정의

- 유니온 타입

  > 특정 파라미터나 변수에 한 가지 이상의 타입을 사용하고 싶을 때 유니온 타입 사용

  ```typescript
  var seho: string | number | boolean;
  
  function logMessage(value: string | number) {
      console.log(value);
  }
  
  logMessage('hello');
  logMessage(100);
  ```

  ```typescript
  function getAge(age: number | string) {
    if (typeof age === 'number') {
      age.toFixed();
      return age;
    }
    if (typeof age === 'string') {
      return age;
    }
    return new TypeError('age must be number or string');
  }
  
  ```

- 인터섹션 타입

  ```typescript
  function askSomeone(someone: Developer & Person) {
      someone.name;
      someone.skill;
      someone.age;
  }
  ```

</br>
</br>

### 이넘

특정 값들의 집합을 의미하는 자료형이다. 타입스크립트에서는 문자형 이넘과 숫자형 이넘을 지원한다.

- 숫자형 이넘

  > 별도의 값을 지정하지 않으면 숫자형 이넘으로 간주된다. 첫번째 값은 0이고, 1씩 증가한다.

  ```typescript
  enum Shoes {
      Nike,
      Adidas
  }
  
  Svar myShoes = Shoes.Nike;
  console.log(myShoes)
  ```

- 문자형 이넘

  ```typescript
  enum Shoes {
      Nike = '나이키',
      Adidas = '아디다스'
  }
  
  var myShoes = Shoes.Nike;
  console.log(myShoes)
  ```

</br>
</br>

### 클래스

클래스란 객체를 정의하는 틀 또는 설계도이다. 클래스를 통해 여러 객체를 생성하여 사용할 수 있다. 타입스크립트에서는 클래스 내부에서 프로퍼티 선언이 가능하다.

```javascript
class Person {
    constructor(name, age) {
        console.log('생성되었습니다.')
        this.name = name;
        this.age = age;
    }
}

var seho = new Person('세호', 30);
```

```typescript
class Person {
    private name: string;
    public age: number;
    readonly log: string;
    
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}
```



