---
title:  "[Javascript] setTimeout, setInterval, and loop delay"
excerpt: "주기적으로 반복하기 위한 js 메서드"

categories:
  - Javascript

last_modified_at: 2020-06-24T18:30:00
---

### WindowOrWorkerGlobalScope
- Wev APIs의 Interface
- Window, WorkerGlobalScope 두 가지 interface에 공통 특징을 뽑아 구성
- setTimeout, setInterval 등의 스케쥴링에 관련된 메서드 존재

### setInterval
- `var intervalID = scope.setInterval(func, [delay, arg1, arg2, ...]);`
- 반복적으로 고정된 시간딜레이 이후 function / code snippet 호출
- interval ID를 반환하여 `clearInterval()` 로 해당 interval 삭제 가능

```js
function timer() {
  let currentTime = new Date().getTime();
  console.log(currentTime);
}

let mInterval = setInterval(timer, 1000);

// 인터벌 멈추고 싶을 때 clearInterval 사용
function stopTimer() {
  clearInterval(mInterval);
}
```

### setTimeout
- `var timeoutID = scope.setTimeout(function[, delay, arg1, arg2, ...]);`
- 타이머 후에 해당 함수를 실행시키는 메서드

```js
function cTime() {
  let currentTime = new Date().getTime();
  console.log(currentTime); 
}

let mTimeout = setTimeout(cTime, 3000);

function stopTime() {
  clearTimeout(mTimeout);
}
```

### loop delay
- 반복문을 딜레이를 주어 실행시키고 싶을 때가 있음
- 예를 들어, 여러 번 반복하는데 각각의 실행에 딜레이를 넣고 싶을 때

```js
for(let i = 0; i < 5; ++i) {
  setTimeout(console.log('Hello World'), 2000);
}
```
- 위와 같은 구조를 생각할 수 있는데, **안 됨**
- 위 스케줄링 함수는 비동기 함수로, 다음 코드를 바로 진행시킴
- 즉, setTimeout 이 5 번 반복되고 2초 뒤에 Hello world가 동시에 출력
- **문제 해결** : setTimeout 를 재귀로 구현

```js
var i = 1;                  //  set your counter to 1

function myLoop() {         //  create a loop function
  setTimeout(function() {   //  call a 3s setTimeout when the loop is called
    console.log('hello');   //  your code here
    i++;                    //  increment the counter
    if (i < 10) {           //  if the counter < 10, call the loop function
      myLoop();             //  ..  again which will trigger another 
    }                       //  ..  setTimeout()
  }, 3000)
}

myLoop();                   //  start the loop
```
- 위와 같이 setTimeout의 파라미터 함수 이용
- 딜레이 후 다시 자기 자신을 호출하는 형태로 딜레이가 있는 반복문 구현

----
**ref :**  
[WindowOrWorkerGlobalScope](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope)  
[Add delay in js loop](https://stackoverflow.com/questions/3583724/how-do-i-add-a-delay-in-a-javascript-loop)
