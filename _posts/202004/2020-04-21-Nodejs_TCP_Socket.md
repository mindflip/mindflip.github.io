---
title:  "[Node.js] TCP Socket - net module"
excerpt: "Node.js 기반 TCP 소켓 통신 구현"

categories:
  - Node.js

last_modified_at: 2020-04-21T18:30:00
---

## net module
- Node.js 기본 모듈인 `net`을 사용하여 소켓 프로그래밍 구현
- stream-based TCP servers/clients를 생성하기 위한 비동기 네트워크 API 제공
- `const net = require('net');`

### methods

| method | description |
|---|---|
| net.createServer([options][, connectionListener]) | creates a new TCP server. returns `net.Server` |
| net.connect(port[, host][, connectListener]) | creates a new net.Socket. after connection, returns `net.Socket` |

- net.Server

| method | description |
|---|---|
| server.listen() | Start a server listening for connections. |
| server.close([callback]) | Stops the server from accepting new connections and keeps existing connections |

| event | description |
|---|---|
| close | Emitted when the server closes. |
| connection | Emitted when a new connection is made. |
| error | Emitted when an error occurs. |
| listening | Emitted when the server has been bound after calling server.listen(). |

- net.Socket

| method | description |
|---|---|
| socket.connect() | Start a server listening for connections. |
| socket.write(data[, encoding][, callback]) | Sends data on the socket. |

| event | description |
|---|---|
| close | Emitted once the socket is fully closed. |
| connect | Emitted when a socket connection is successfully established. |
| data | Emitted when data is received. |
| error | Emitted when an error occurs. |


### example source code (Echo)

- Server

```js
const net = require('net');
const server = net.createServer((connection) => { // createServer는 net.Socket 클래스 반환
  console.log('client connected');
   
  connection.on('end', () => {    // client 커넥션이 끊기면 호출되는 이벤트
    console.log('client disconnected');
  });

  connection.pipe(connection);    // 소켓의 데이터를 그대로 전달 (echo 역할)
});

server.listen(8090, () => {   // 다른 소켓의 접속 listening
  console.log('server is listening');
});
```

- Client

```js
const net = require('net');
const client = net.connect({port: 8090}, () => {  // connect는 net.Socket 클래스 반환
    console.log("client connected");    
});

client.write("client send data");   // tx 버퍼에 data 쓰기

client.on('data', (data) => {   // rx 버퍼에 데이터 읽어오기
    console.log("msg from server : " + data.toString());
    client.end();
});

client.on('end', () => {    // 연결 끊김 확인
    console.log("disconnected from server");
});
```

----
**ref**  
[[Node.js Doc] Net](https://nodejs.org/api/net.html)  
[TCP 서버 및 클라이언트](https://namik.tistory.com/114)  

