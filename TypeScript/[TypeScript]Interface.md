# Interface

### interface

타입스크립트에서는 type과 interface를 사용하여 객체의 타입을 정의하고, 사용할 수 있다. 인터페이스는 일반적으로 타입 체크를 위해 사용되며 변수, 함수, 클래스에 사용할 수 있다. type과 interface 모두 객체의 타입과 이름을 지정한다는 점에서 공통점이 있지만 type은 선언적 확장이 불가능하다는 점에서 차이가 있다.

인터페이스에 선언된 프로퍼티 또는 메소드의 구현을 강제하여 일관성을 유지할 수 있도록 한다. ES6는 인터페이스를 지원하지 않지만 TypeScript에서는 사용할 수 있다. TypeScript 공식 문서에서는 인터페이스의 사용을 권장한다.

</br>

</br>

### Type과 Interface

```typescript
// interface
intereface student {
  id: number;
  name: string;
};

const interfaceStudent: student = {
  id: 170,
  name: '슬기',
};

// type
type student = {
  id: number;
  name: string;
};

const typeStudent: student = {
  id: 270,
  name: '슬기'
}
```

</br>

</br>

### 함수와 인터페이스

```typescript
interface interFunc {
  (num: number): number;
}

const interfaceFunc: interFunc = function (num: number) {
  return num * num;
}

console.log(interfaceFunc(10));
```

</br>

</br>

### 선언적 확장

```typescript
interface student {
  no: number;
}

interface student {
  // 선언적 확장
  name: string;
}

const tiger: student = {
  no: 201,
  name: "슬기",
};

console.log(tiger);

type _student = {
  no: number;
};

type _student = {
  // error : 식별자 중복
  name: string;
};
```

인터페이스와 타입의 가장 큰 차이점인 선언적 확장이다. 인터페이스는 같은 이름을 가진 `student` 로 no, name등 속성을 확장할 수 있지만 타입은 같은 이름을 두번 선언할 시 에러가 발생한다.

</br>

</br>

### 어떤 것을 사용해야 할까

union 혹은 튜플과 같이 type에서만 사용할 수 있는 것들을 써야 하는 경우에는 type을 쓰고, 그 외에는 interface를 사용한다. 또한 팀 혹은 프로젝트 방향에서 type이나 interface 정해서 일관성 있게 사용하는 것이 좋다.