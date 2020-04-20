---
title:  "[Network] TCP Socket communication"
excerpt: "소켓의 개념과 TCP 연결 과정"

categories:
  - Network

last_modified_at: 2020-04-20T18:30:00
---

### Socket 정의
![socket](/assets/images/posts/200420/socket_door.jpg)
- 소켓은 통신의 소프트웨어적 개념
- 어플리케이션이 TCP/IP 네트워크에 연결할 수 있도록 함
- 특정 호스트의 어플리케이션은 소켓을 생성하고, 다른 호스트의 어플리케이션에 연결
- 앱 사이의 메시지들은 소켓을 거쳐감

### Virtual TCP/UDP connections
![sockets](/assets/images/posts/200420/sockets.png)
- 소켓은 호스트 사이의 가상 TCP/UDP 채널 역할
- 앱이 실행되면 포트 번호가 부여
- 다른 호스트와 통신하고 싶을 때 소켓 생성
- 위의 예는 3가지 앱이 3가지 TCP 채널을 이용해 통신하는 모습

### TX & RX buffers
![socket buffers](/assets/images/posts/200420/socket_buffers.png)
- 소켓은 송신/수신 메모리 버퍼로서 물리적으로 구현
- 프로세스는 메세지를 transmit buffer에 write
- 같은 주기로 다른 호스트의 프로세스가 receive buffer 확인
- Transport layer가 receive buffer에 메시지를 write 함으로써 메시지 전송
- Transport layer는 주기적으로 소켓의 tx buffer를 체크하여 보낼 메시지 있는지 결정

### TCP connection/disconnection
![tcp state](/assets/images/posts/200420/tcpstate.png)
1. 3-way handshake (connection establish)
  - server : 소켓 생성 -> binding(소켓에 ip 할당하는 과정) -> listening(client의 연결 대기)
  - client : 소켓 생성 -> connect -> 3-way handshake 시작
  - SYN(c-s) -> SYN/ACK(s-c)(established) -> ACK(c-s)
2. data transfer
  - client tx 버퍼에 메시지 write
  - trnaport layer 통해 server rx 버퍼에 메시지 write
  - server rx 버퍼 메시지 read
  - 반대동작 동일
3. 4-way handshake (connection termination)
  - client : close
  - FIN(c-s) -> ACK(s-c) -> FIN(s-c) -> ACK(c-s)

----
**ref**  
[Sockets](https://microchipdeveloper.com/tcpip:tcp-ip-sockets)  
[TCP의 데이터 보장 원리에 대해 파헤쳐보기](https://velog.io/@jyongk/TCP%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%B4%EC%9E%A5%EC%84%B1-%EB%8C%80%ED%95%B4-%ED%8C%8C%ED%97%A4%EC%B3%90%EB%B3%B4%EC%9E%90-m0k4vchxup#%ED%85%8C%EC%8A%A4%ED%8A%B8)  
[TCP/IP 네트워크 스택 이해하기](https://d2.naver.com/helloworld/47667ㅇ)  
