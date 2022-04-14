# Redux-saga

### redux-saga

- 정의 : 액션을 모니터링하고 있다가, 특정 액션이 발생하면 이에 따라 특정 작업을 하는 방식

  > 특정 작업 : 특정 자바스크립트 실행, 다른 액션을 디스패치, 현재 상태 불러오는 것

- 특징

  - 비동기 작업을 할 때 기존 요청 취소 처리 가능
  - 특정 액션이 발생했을 때 이에 따라 다른 액션이 디스패치되게끔 하거나, 자바스크립트 코드를 실행
  - 웹소켓을 사용하는 경우 채널이라는 기능을 사용하여 더욱 효율적으로 코드 관리
  - API 요청이 실패했을 때 재요청하는 작업 가능



### Generator

함수에서 값을 순차적으로 반환 가능

```javascript
function* generatorFunction() {
    console.log('안녕하세요?');
    yield 1;
    console.log('제너레이터 함수');
    yield 2;
    console.log('function*');
    yield 3;
    return 4;
}

const generator = generatorFunction();              // 제너레이터 생성
generator.next()                                    // 제너레이터 호출
```

- fuction* : 제너레이터 함수 만들 때 fuction* 키워드 사용

- 제너레이터 함수 호출 시 반환되는 객체가 제너레이터

  > 호출 시 인자 전달하여 제너레이터 함수 내부에서 사용할 수 있음

- 제너레이터 호출 시 yield 값 반환하고 코드의 흐름 멈추게 됨