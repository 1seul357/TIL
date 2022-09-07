# Interface

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
  // errolr : 식별자 중복
  name: string;
};
```

### interface

인터페이스는 상호 간에 정의한 약속 혹은 규칙이다. 객체의 타입과 이름을 지정할 수 있다. type과 interface 모두 객체의 타입과 이름을 지정한다는 점에서 공통점이 있지만 type은 선언적 확장이 불가능하다는 점에서 차이가 있다. 또한 interface는 객체에서만 사용이 가능하다.

</br>

</br>

### 어떤 것을 사용해야 할까

union 혹은 튜플과 같이 type에서만 사용할 수 있는 것들을 써야 하는 경우에는 type을 쓰고, 그 외에는 interface를 사용한다. 또한 팀 혹은 프로젝트 방향에서 type이나 interface 정해서 일관성 있게 사용하는 것이 좋다.