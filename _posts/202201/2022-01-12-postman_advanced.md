---
title: "[postman] postman을 이용한 로그인 검증"
excerpt: "postman advanced"

categories:
  - postman

last_modified_at: 2021-01-12T13:00:00
---

- 로그인 과정에는 본인을 검증하기 위한 authentication process가 동반
- 브라우저에서는 로그인 정보가 쿠키나 세션에 저장되어 인증 기반 데이터 요청에 사용
- 브라우저 없이 postman으로 인증을 검증하는 방법을 알아보기

### postman environment setting

- 왼쪽의 Environments 탭에서 사용할 environment setting 추가
- variable에 url, authToken 추가
- url의 initial value, current value에 localhost:3000 설정
- postman 환경 변수들은 \{\{envname}} 으로 사용 가능

### collection 생성 및 설정

- collection은 endpoint의 모음집
- 설정에 `Authorization` 탭 클릭
- Type 설정에서 `Bearer Token` 선택
  - jwt에 적합한 설정
  - 모든 요청에 이 auth 방식을 사용
- Token 설정에 \{\{authToken}} 입력
- 이후 request header에 `Bearer tokenstring`이 자동 삽입

### requests 설정

- create, login api 생성
- \{\{url}}을 여기서 이용
- api 설정에 Test 탭 클릭
- 아래와 같은 내용 설정
- 201 or 200 응답이면 `authToken` 변수에 token 값을 넣겠다는 의미

```js
// 201 for creat, 200 for login
if (pm.response.code === 201) {
  pm.environment.set("authToken", pm.response.json().token);
}
```

- create, login을 하면 environment의 authToken의 값이 해당 토큰으로 갱신되어있는지 체크
- 이후 authentication이 필요한 api에서 검증해보기

---

**ref :**  
[Authorizing requests](https://learning.postman.com/docs/sending-requests/authorization/){:target="\_blank"}
