---
title:  "[HTTP] Response status code"
excerpt: "자주 사용하는 http 응답상태코드 정리"

categories:
  - HTTP

last_modified_at: 2020-07-29T18:30:00
---

## 대역별 코드 정리
- http 상태코드는 http request가 성공적으로 완료되었는지에 대한 판단
1. 정보 응답 (100-199)
2. 성공 응답 (200-299)
3. 리다이렉션 (300-399)
4. 클라이언트 오류 (400-499)
5. 서버 오류 (500-599)


### 정보 응답 (Information responses)
- 100 Continue
  - 중간 단계 응답. 현재까지 문제가 없음기에 계속해서 클라이언트가 요청을 해도 된다는 의미

### 성공 응답 (Successful responses)
- 200 OK
  - 요청이 성공했을 때
  - HTTP method에 따른 성공의 의미
  - `GET` : 리소스를 읽어들여, 메시지 바디로 전송됨
  - `HEAD` : 엔티티의 헤더가 메시지 바디 안에 있음
  - `PUT` or `POST` : 리소스가 메시지 바디에 담겨 전송됨
  - `TRACE` : 메시지 바디가 서버로 부터 받은 요청메시지를 포함하고 있음
- 201 Created
  - 요청이 성공하고, 새로운 리소스가 결과로 생성됨
  - 주로 POST, PUT 요청의 응답으로 사용
- 202 Accepted
  - 요청이 수신됐지만, 아직 액션은 이루어지지 않음

### 리다이렉션 (Redirection messages)
- 300 Multiple Choice
  - 요청이 여러 응답을 만족할 때
  - 사용자는 하나를 선택해야함
- 301 Moved Permanently
  - 요청된 리소스의 URL이 영구적으로 변경됨
  - 새로운 URL을 응답에 넣음
- 302 Found
  - 임시로 URI를 변경

### 클라이언트 오류 (Client error responses)
- 400 Bad Request
  - 서버가 타당하지 않은 구문이 있는 요청을 해석하지 못 할 경우
- 401 Unauthorized
  - 클라이언트가 인증을 제대로 하지 못 한 경우
- 403 Forbidden
  - 클라이언트가 컨텐트에 엑세스 권한이 없는 경우
  - 401과 다르게 클라이언트 identity는 알고 있음
- 404 Not Found
  - 서버가 요청 리소스를 찾을 수 없을 때
  - 즉, URL을 인지 못 할 때
- 405 Method Not Allowed
  - 서버가 요청 메서드는 알지만, 사용이 금지된 경우
- 408 Request Timeout
  - 쉬고 있는 커넥션에 응답을 보낸 경우
  - 서버는 사용하지 않는 커넥션을 닫을 수도 있음
- 410 Gone
  - 요청된 컨텐트가 서버에서 영구적으로 삭제된 경우
  - 클라이언트는 그 리소스의 캐시를 삭제하기를 권장됨

### 서버 오류 (Server error responses)
- 500 Internal Server Error
  - 서버가 이해하지 못 하여 처리가 안 되는 상황일 때
- 501 Not Implemented
  - 요청 메서드가 서버에서 지원되지 않아 처리되지 않을 때
- 502 Bad Gateway
  - 게이트웨이로 사용되는 서버가 타당하지 않은 응답을 받았을 때
- 503 Service Unavailable
  - 서버가 요청 처리 준비되지 않았을 때
- 504 Gateway Timeout
  - 게이트웨이로 사용되는 서버가 응답을 제시간에 받지 못 했을 때


----
**ref :**  
[HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)  
