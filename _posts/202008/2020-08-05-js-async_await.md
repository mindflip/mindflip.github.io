---
title:  "[Javascript] 비동기 처리에 필수적인 async / await"
excerpt: "async / await 개념 및 예제"

categories:
  - Javascript

last_modified_at: 2020-08-05T18:30:00
---

### async / await 사용하는 이유?
- 비동기 처리 패턴
- 콜백함수, 프로미스의 단점 보완

### 비동기 처리가 필요한 순간
- 외부 리소스를 가져올 때(I/O 작업)
  - ex) http, database request / response, file I/O
- setTimeout() 등의 비동기 함수

### Callback Hell
- callback을 이용한 비동기 처리를 연달아 해야하는 구문은 코드가 깊어짐
- 코드를 얕게 유지하는 것이 필요
- 얕은 코드는 각 모듈의 의존성을 낮추어 가독성/유지보수효율 높일 수 있음

```javascript
firstFunction(args, function() {
  secondFunction(args, function() {
    thirdFunction(args, function() {
      // And so on…
    });
  });
});
```

### Promise
- callback hell을 해결하기 위해 고안
  - 콜백들을 모듈화하여 해결할 수도 있지만, 직관적이지 않음
- 작업 후 실행하는 callback과 다르게, Promise 자체 메소드인 `.then()` 사용

```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData().then(function(data) {
  console.log(data); // response 값 출력
}).catch(function(err) {
  console.error(err); // Error 출력
});
```

### async / await
- async 함수는 Promise를 리턴
- await는 비동기 함수가 끝날때까지 대기시킴
- await는 async 함수 안에서만 사용 가능
- await는 Promise의 resolve 값을 리턴 받음
- 다른 방식들보다 간결한 코드, 직관적
- try/catch 이용한 error handling

```javascript
function fetchUser() {
  var url = 'https://jsonplaceholder.typicode.com/users/1'
  return fetch(url).then(function(response) {
    return response.json();
  });
}

function fetchTodo() {
  var url = 'https://jsonplaceholder.typicode.com/todos/1';
  return fetch(url).then(function(response) {
    return response.json();
  });
}
```

```javascript
async function logTodoTitle() {
  try {
    var user = await fetchUser();
    if (user.id === 1) {
      var todo = await fetchTodo();
      console.log(todo.title); // delectus aut autem
    }
  } catch (error) {
    console.log(error);
  }
}
```

----
**ref :**  
[Callback Hell](http://callbackhell.com/)  
[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)  
[[MDN]async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)  