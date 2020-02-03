---
title:  "[Network] Web Socket"
excerpt: "양방향 통신이 가능한 웹소켓 프로토콜"

categories:
  - Network

last_modified_at: 2020-02-03T18:30:00
---

- **리눅스 기반 ROS**와 **윈도우 기반 Unity**에서 통신이 필요한 상황 발생
- ROS에서 Web Socket 기반의 통신을 제공하는 rosbridge_suite 라이브러리 필요
- Web Socket이 정확히 뭐지?

### Web Socket
![web socket1](/assets/images/posts/200203/ws1.png)
- 두 프로그램간 메시지를 교환하기 위한 통신 방법
- W3C / IETF에 의해 자리 잡은 표준 프로토콜
- 양방향 통신(Full Duplex) : client-server 송수신 동시에 처리
- 실시간 네트워킹(Real Time-Networking) : 웹환경에서 채팅, 스트리밍 등의 작업에 적합

### 동작방식
![web socket message exchange](/assets/images/posts/200203/ws2.png)
1. Client가 handshake 요청 메시지를 Server로 전송
2. Server는 handshake 메시지에 응답
3. Web Socket 연결 성공
4. C-S 사이에 data payload frames / close frame 통신

### 특징
- 최초 접속에만 HTTP 프로토콜을 이용해 Handshaking
- web socket을 위한 별도의 포트 X (기존 http-80 or https-443 사용)
- ws - http 기반 / wss - https 기반 (ex. ws://192.168.1.15:9090)
![framing protocol](/assets/images/posts/200203/ws_protocol.png)


----
**ref**  
[웹 소켓 통신 (Web Socket)](https://caileb.tistory.com/185)  
[WebSocket 기반 실시간 양방향 통신.](https://jusungpark.tistory.com/40)  
[Websocket Protocol 분석](https://swiftymind.tistory.com/104)  
[How JavaScript works: Deep dive into WebSockets and HTTP/2 with SSE + how to pick the right path](https://blog.sessionstack.com/how-javascript-works-deep-dive-into-websockets-and-http-2-with-sse-how-to-pick-the-right-path-584e6b8e3bf7)
[RFC6455](https://tools.ietf.org/html/rfc6455)  