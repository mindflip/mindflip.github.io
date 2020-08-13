---
title:  "[Node.js] dotenv (npm)"
excerpt: "Node.js에서 환경변수 설정을 위한 dotenv 라이브러리"

categories:
  - Javascript
  - Node.js

last_modified_at: 2020-08-13T19:00:00
---

### 환경변수
- 특정 process를 위한 key-value 형태의 변수
- 환경변수에 따라 개발/운영/테스트 구분하여 관리 가능

### process.env
- Node로 실행한 앱에는 process라는 변수에 다양한 정보 존재
- `process.env`

```json
{
    ...
    TERM_PROGRAM: 'Apple_Terminal',
    GEM_HOME: '/Users/pnu/.rvm/gems/ruby-2.6.3',
    SHELL: '/bin/bash',
    TERM: 'xterm-256color',
    TERM_PROGRAM_VERSION: '433',
    MY_RUBY_HOME: '/Users/pnu/.rvm/rubies/ruby-2.6.3',
    USER: 'pnu',
    ...
}

```

- 환경변수 설정

```
윈도우 / set NODE_ENV=test
리눅스 / export NODE_ENV=test
```

- 환경변수를 이용해 상황에 따른 코드사용이 가능

```js
if (process.env.NODE_ENV === "test") {
  env = "테스트환경";
} else if (process.env.NODE_ENV === "dev") {
  env = "개발환경";
}
```

### dotenv
- 별도의 파일로 운영환경에 따라 각종 정보를 관리
- `npm i dotenv`

```
// .env
deploy_status=productionPicked

// .env.dev
deploy_status=developmentPicked
```

```js
const env = require('dotenv')

env.config({ 
    path : path.resolve(
        process.cwd(),
        process.env.NODE_ENV == "production" ? ".env" : ".env.dev"
    )
});

console.log(process.env.deploy_status);

/*
set NODE_ENV=productoin
will print out 'productionPicked'

set NODE_ENV=development (or any other values execpt 'production')
will print out 'developmentPicked'
*/
```

- 사용예시)
- jest script 설정을 아래와 같이 작성 후 테스팅
- `NODE_ENV=test jest --watchAll`
- 위의 환경변수에 맞춰 test database config 설정

----
**ref :**  
[[DOC] Node.js - process](https://nodejs.org/api/process.html#process_process_env)  
[Environment Variables](https://github.com/lorenwest/node-config/wiki/Environment-Variables)  
[dotenv](https://github.com/motdotla/dotenv#readme)  
[NodeJS 환경 변수 설정](https://devhyun.com/blog/post/23)  
