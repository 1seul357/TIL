# Node.js

### Node

비동기 (Asynchronous) 이벤트 기반 JavaScript 런타임 환경이다.

노드를 통해 다양한 자바스크립트 애플리케이션을 실행할 수 있으며 서버를 실행하는데 가장 많이 사용된다.

- Node.js는 JavaScript를 서버에서도 사용할 수 있도록 만든 프로그램이다.
- Node.js는 V8이라는 JavaScript 엔진 위에서 동작하는 자바스크립트 런타임 환경이다.
- Node.js는 서버사이트 스크립트 언어가 아니다. 프로그램 (환경) 이다.
- Node.js는 웹서버와 같이 확장성 있는 네트워크 프로그램을 제작하기 위해 만들어졌다.

</br>

</br>

### Node.js 특징

- 비동기 IO 처리, 이벤트 위주 : 모든 API는 비동기 처리된다. 데이터를 반환할 때까지 기다리지 않고, 다음 API를 실행한다.
- 빠른 속도 : V8 자바스크립트 엔진을 사용하여 빠른 코드 실행을 제공한다.
- 단일 thread / 확장성

</br>

</br>

### 패키지 생성 및 초기화

```bash
npm itit
```

해당 명령어를 입력하면 package.json 파일이 생성된다.

```json
{
 "name": "node-practice",
 "version": "1.0.0",
 "description": "",
 "main": "index.js",
 "scripts": {
   "test": "echo \"Error: no test specified\" && exit 1"
},
 "author": "",
 "license": "ISC"
}
```

</br>

</br>

### Express.js 설치

```bash
npm install express
```

package.json의 "dependencies"에 express가 추가되고, package-lock.json 파일이 생성된다.

```json
...
 "dependencies": {
   "express": "^4.18.1"
}
...
```

</br>

</br>

### 서버 구축

```javascript
const express = require('express');
const app = express();
const port = 8080;

// 지정된 경로에 대한 모든 유형의 HTTP 요청에 대해 실행
app.get('/', (req, res) => {
   res.send("Hello Node.js");
});

// 지정된 port, host로 접속할 수 있게 바인드(bind) 하고, 대기(listen)
app.listen(port, () => {
   console.log("Listening...");
});
```

</br>

</br>

### 실행

```bash
node index.js
```