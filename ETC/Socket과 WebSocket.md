# Socket과 WebSocket

컴퓨터에서 프로그램이 네트워크에서 데이터를 통신할 수 있도록 연결해주는 것이다. 메시지를 보내는 쪽 (Client Socket)과 받는 쪽 (Server Socket) 모두 Socket이 열려 있으면 데이터를 보내고, 받을 수 있다.

**Client Socket** : 통신 연결 요청을 보내는 것

**Server Socket** : 통신 연결 요청을 받는 것

</br>

</br>

### Client Socket의 처리 흐름

#### 1. Client Socket 생성

연결 대상에 대한 정보가 들어있지 않은 Socket을 생성한다.


#### 2. 연결 요청 (Connection)

연결하고 싶은 대상에게 요청을 보낸다. IP 주소와 포트 번호로 연결하고 싶은 대상을 특정한다. 요청을 보내면 요청에 대한 결과가 돌아오는데, 이때 Connect의 실행이 끝난다.


#### 3. 데이터의 송수신 (Send, Recieve)

- 송신(Send) 시 데이터를 보내는 것이므로 데이터를 언제, 얼마나 보낼 것인지 알 수 있다.
- 수신(Recieve) 할 때에는 상대방이 언제, 얼만큼의 데이터를 보낼 것인지 알 수 없다.
- 수신하는 API는 별도의 Thread에서 진행하게 된다.


#### 4. Socket 닫기

더 이상의 데이터 송수신이 필요없어지면 소켓을 닫는다.

</br>

</br>

### Server Socket의 처리 흐름

#### 1. Server Socket 생성 (socket)

Client Socket 생성 시와 마찬가지로, 연결 대상에 대한 정보가 들어있지 않은 껍데이 Socket을 생성한다.


#### 2. Server Socket 바인딩 (bind)

Socket과 Port 번호를 바인딩한다. 

여러가지의 프로세스가 동시에 실행될 때, 각 프로세스를 구분하기 위해서 Socket과 Port 번호를 결합 (Bind) 하는 작업이 필요하다. 하나의 프로세스는 같은 Port를 가진 Socket을 여러개 열 수 있다.


#### 3. Client 연결 요청 대기 (listen)

Server Socket에서 Port 번호와 바인딩 작업이 끝나면 Client로부터의 연결 요청을 받을 준비가 된 것이다. Client가 연결 요청을 할 때까지 계속 기다리면서 연결 요청이 오면 대기 상태를 종료하고, 리턴한다.


#### 4. Client 연결 수립 (accept)

실직적인 연결이 이루어진다. 연결 요청을 받아들여 소켓 간의 연결을 수립한다. 중요한 점은 클라이언트 소켓과 연결이 만들어지는 소켓은 앞에서 사용한 서버 소켓이 아닌 accpet API 내부에서 새로 만들어지는 소켓이라는 점이다. 앞에서 사용한 서버 소켓은 또 다른 연결 요청을 처리하기 위해 다시 대기(listen)하거나 서버 소켓을 닫는(close) 역할을 한다.


#### 5. 데이터의 송수신 (Send, Recieve)

- 송신(Send) 시 데이터를 보내는 것이므로 데이터를 언제, 얼마나 보낼 것인지 알 수 있다.
- 수신(Recieve) 할 때에는 상대방이 언제, 얼만큼의 데이터를 보낼 것인지 알 수 없다.
- 수신하는 API는 별도의 Thread에서 진행하게 된다.


#### 6. Socket 닫기

더 이상의 데이터 송수신이 필요없어지면 소켓을 닫는다. 서버 소켓은 Client와의 연결 수립에서 생성된 새로운 소켓에 대해서도 관리를 해야 한다.

</br>

</br>

### WebSocket

WebSocket은 Web에서 두 프로그램 간의 메시지를 교환하기 위한 통신 방법 중 하나이다. 

IP, Port 통신을 한다는 점은 같지만 웹 브라우저는 HTTP Protocol, 소켓은 TCP/IP 프로토콜을 사용한다는 점에서 차이가 있다. 웹 브라우저는 HTTP Protocol을 사용하므로 실시간 통신을 할 수 없는데, 이러한 문제를 해결하기 위해 WebSocket Protocol을 사용한다.

</br>

</br>

### WebSocket 동작 방법

#### 1. HandShaking

브라우저와 서버의 연결을 시작하게 해주는 단계이다. 최초로 접속할 때에 HTTP Protocol 위에서 HandShaking을 하기 때문에, HTTP Header를 사용한다.

WebSocket을 호출하여 Socket을 생성하면 즉시 연결이 시작되고, 연결이 유지되는 동안 브라우저는 Header를 통해 서버에 WebSocket을 지원하는지 물어본다. 이때 서버가 맞다는 응답을 하면 HTTP Protocol 대신 WebSocket Protocol로 통신된다.


#### 2. Data Transfer

WebSocket 연결이 되면 데이터를 송수신 할 수 있다. 


#### 3. Close HandShaking

데이터의 송수신이 완료되면 Client와 Server 모두 Connection을 종료하기 위한 프레임을 전송한다.

</br>

</br>

### Socket.io

이러한 웹 소켓을 쉽게 구현할 수 있는 라이브러리가 있는데, 이것이 바로 Socket.io 이다.

Socket.io는 웹소켓을 활용하여 만든 라이브러리이고 실시간, 양방향 통신을 지원한다. (서버 <=> 클라이언트)

- **socket.connect()**: 소켓 연결.
- **socket.emit("이벤트 명", Data)**: 이벤트 명을 지정하고 데이터를 보냄.
- **socket.on("이벤트 명", 콜백 함수)**: 해당 이벤트를 받고 콜백함수를 실행.
- **socket.disconnect()**: 소켓 연결을 끊음.

</br>

</br>

### io와 socket

io는 **전체 클라이언트**와의 상호작용을 위한 객체이다. 반면 socket은 **개별 클라이언트**와의 상호작용을 위한 객체이다.

</br>

</br>

### Server-side

**클라이언트로부터 메시지 수신**

```
// 전체 클라이언트로부터의 메시지 수신
io.on('connection', function(socket) {

});

// 특정 클라이언트로부터의 메시지 수신
socket.on('connection', function(socket) {

});
```

**클라이언트에게 메시지 송신**

| Method                | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| io.emit               | 접속된 모든 클라이언트에게 메시지를 전송한다.                |
| socket.emit           | 메시지를 전송한 클라이언트에게만 메시지를 전송한다.          |
| socket.broadcast.emit | 메시지를 전송한 클라이언트를 제외한 모든 클라이언트에게 메시지를 전송한다. |
| io.to(id).emit        | 특정 클라이언트에게만 메시지를 전송한다. id는 socket 객체의 id 속성값이다. |
| event name            | 이벤트 명 (string)                                           |
| msg                   | 송신 메시지 (string or object)                               |

```
// 접속된 모든 클라이언트에게 메시지를 전송한다.
io.emit('event_name', msg);

// 메시지를 전송한 클라이언트에게만 메시지를 전송한다.
socket.emit('event_name', msg);

// 메시지를 전송한 클라이언트를 제외한 모든 클라이언트에게 메시지를 전송한다.
socket.broadcast.emit('event_name', msg);

// 특정 클라이언트에게만 메시지를 전송한다.
io.to(id).emit('event_name', data);
```

</br>

</br>

### Client-side

**서버에게 메시지 송신**

| Parameter  | Description                    |
| ---------- | ------------------------------ |
| event name | 이벤트 명 (string)             |
| msg        | 송신 메시지 (string or object) |

```
socket.emit("event_name", msg);
```

**서버로부터 메시지 수신**

| Parameter  | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| event name | 서버가 메시지 송신 시 지정한 이벤트 명 (string)              |
| function   | 이벤트 핸들러. 핸들러 함수의 인자에 서버가 송신한 메시지가 전달된다. |

```
socket.on("event_name", function(data) {
 console.log('Message from Server: ' + data);
});
```

</br>

</br>

### 구현하기

```javascript
// index.js = server
const express = require("express"); // 웹 서버 프레임워크
const app = express();
const http = require("http");
const server = http.createServer(app); // server 객체 생성
const { Server } = require("socket.io");
const io = new Server(server); // 소켓 통신 담당

// '/' 경로의 요청에 대하여 '/index.html' 파일을 보낸다는 뜻이다.
// emit은 던지기, on은 받기!
app.get("/", (req, res) => {
 res.sendFile(__dirname + "/index.html");
});

// connection을 클라이언트(브라우저)로부터 받으면 실행되는 부분이다.
io.on("connection", (socket) => {
 socket.broadcast.emit("hi");
});

// 클라이언트로부터 chat message 라는 이벤트를 받으면 msg 확인할 수 있다.
io.on("connection", (socket) => {
 socket.on("chat message", (msg) => {
   // 서버 -> 클라이언트로 Emit 하기. 받은 msg 'emit'하기
   io.emit("chat message", msg);
   console.log(msg);
});
});

// 8080번 포트를 통해 통신
server.listen(8080, () => {
 console.log("listening on * : 8080");
});

// 서버의 모든 사용자에게 이벤트 보내기
io.emit("some event", {
 someProperty: "some value",
 otherProperty: "other value",
});

```

```javascript
<!-- index.html = 브라우저에 표시될 내용이 적힌 파일 -->
<!DOCTYPE html>
<html>
 <head>
   <title>Socket.IO chat</title>
   <style>
     body {
       margin: 0;
       padding-bottom: 3rem;
       font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
         Helvetica, Arial, sans-serif;
    }
     #form {
       background: rgba(0, 0, 0, 0.15);
       padding: 0.25rem;
       position: fixed;
       bottom: 0;
       left: 0;
       right: 0;
       display: flex;
       height: 3rem;
       box-sizing: border-box;
       backdrop-filter: blur(10px);
    }
     #input {
       border: none;
       padding: 0 1rem;
       flex-grow: 1;
       border-radius: 2rem;
       margin: 0.25rem;
    }
     #input:focus {
       outline: none;
    }
     #form > button {
       background: #333;
       border: none;
       padding: 0 1rem;
       margin: 0.25rem;
       border-radius: 3px;
       outline: none;
       color: #fff;
    }
     #messages {
       list-style-type: none;
       margin: 0;
       padding: 0;
    }
     #messages > li {
       padding: 0.5rem 1rem;
    }
     #messages > li:nth-child(odd) {
       background: #efefef;
    }
   </style>
 </head>
 <body>
   <ul id="messages"></ul>
   <form id="form" action="">
     <input id="input" autocomplete="off" /><button>Send</button>
   </form>
   <script src="/socket.io/socket.io.js"></script>
   <script>
     var socket = io(); // io 객체 생성

     var messages = document.getElementById("messages");
     var form = document.getElementById("form");
     var input = document.getElementById("input");

     form.addEventListener("submit", function (e) {
       e.preventDefault();
       if (input.value) {
         // 메시지 보내기 누르면 서버에게 'chat message' 이벤트 전송
         socket.emit("chat message", input.value);
         input.value = "";
      }
    });

     // 서버가 emit 한 메시지 받고(on), 브라우저에 출력하기
     socket.on("chat message", function (msg) {
       var item = document.createElement("li");
       item.textContent = msg;
       messages.appendChild(item);
       window.scrollTo(0, document.body.scrollHeight);
    });
   </script>
 </body>
</html>
```

