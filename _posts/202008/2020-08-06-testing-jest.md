---
title:  "[Testing] Jest - javascript testing framework"
excerpt: "express unit test를 위한 jest 사용기"

categories:
  - Javascript
  - Node.js
  - Testing

last_modified_at: 2020-08-06T19:30:00
---

### Jest
- 자바스크립트 테스팅 프레임워크
- 2019년에 가장 많이 사용한 js 테스팅 툴 [(참고)](https://2019.stateofjs.com/testing/)

### 특징
- 각기 다른 js 프로젝트에서의 맞춤 설정이 필요 없음
- 스냅샷 테스팅 : UI 변경에 유용
- 테스팅은 프로그램 실행과 병렬적으로 진행 (독립적)
- api가 잘 돼있음

## node.js express testing
- `Todo list` tdd 개발
- 예제를 이용해 api 설명
- jest와 함께 사용한 테스팅 라이브러리
  - `supertest` : API integration test. HTTP 검증 도구로 사용
  - `node-mocks-http` : express에서 테스팅을 위한 http mock object 생성
- pakage.json 의 script > test 값을 `jest --watchAll` 로 변경
- `npm run test` 명령어로 테스트 실행

### Unit Test POST(create)

```javascript
describe("TodoController.createTodo", () => {

    beforeEach(() => {
        req.body = newTodo;
    });

    it("should have a createTodo function", () => {
        expect(typeof TodoController.createTodo).toBe("function");
    });

    it("should call TodoModel.create", () => {
        TodoController.createTodo(req, res, next);
        expect(TodoModel.create).toBeCalledWith(newTodo);
    });

    it("should return 201 response code", async () => {
        await TodoController.createTodo(req, res, next);
        expect(res.statusCode).toBe(201);
        expect(res._isEndCalled()).toBeTruthy();
    });

    it("should return json body in response", async () => {
        TodoModel.create.mockReturnValue(newTodo);
        await TodoController.createTodo(req, res, next);
        expect(res._getJSONData()).toStrictEqual(newTodo);
    });

    it("should handle errors", async () => {
        const errorMessage = { message : "Done property missing"};
        const rejectedPromise = Promise.reject(errorMessage);
        TodoModel.create.mockReturnValue(rejectedPromise);
        await TodoController.createTodo(req, res, next);
        expect(next).toBeCalledWith(errorMessage);
    });
});
```

- `describe` : 테스팅 블록. 관련된 테스트를 그룹화하여 관리
- `beforeEach()` : 각 유닛 테스트가 실행되기 전, 수행되는 작업. 함수가 promise를 반환하면, resolve 될 때까지 테스팅 대기
- `it` : `test`와 같음. 각 기능에 대한 단위 테스팅
- `expect` : 값을 테스트하기 위해 사용 (제일 중요). 아래의 matcher와 함께 호출.
  - `toBe(Value)` : 원시 값, 또는 인스턴스의 identity 확인을 위해 사용. 비교를 위해 `Object.is` 호출
  - `toHaveBeenCalled()` : `toBeCalled()` 와 같음. mock function이 호출 되었는지 체크
  - `toHaveBeenCalledWith(arg1, arg2, ...)` : `toBeCalledWith()` 와 같음. mock function이 특정 argument와 같이 호출되었는지 체크
  - `toBeTruthy()` : 결과의 값 보다는, 참인지 아닌지 체크
  - `toStrictEqual(Value)` : 오브젝트들이 구조를 포함하여 같은 타입을 가지고 있는지 체크
- req, res에 node-mocks-http 라이브러리 사용하여 mock fucntion 부여
- TodoModel의 각종 메서드에 mock function(jest.fn()) 부여

### Integration Test POST(create)

```javascript
describe(endpointUrl, () => {
    it("POST " + endpointUrl, async () => {
        const response = await request(app)
        .post(endpointUrl)
        .send(newTodo);
        expect(response.statusCode).toBe(201);
        expect(response.body.title).toBe(newTodo.title);
        expect(response.body.done).toBe(newTodo.done);
        newTodoId = response.body._id;
    });
    it("should return error 500 on malformed data with POST" + endpointUrl,
    async () => {
        const response = await request(app)
        .post(endpointUrl)
        .send({title : "Missing done property"});
        expect(response.statusCode).toBe(500);
        expect(response.body).toStrictEqual({
            message : "Todo validation failed: done: Path `done` is required."
        });
    });
});
```

- `supertest` 라이브러리를 이용한 api 통합테스트
- `request()` http 메서드를 이용해서 요청에 따른 응답 테스팅

----
**ref :**  
[JEST](https://jestjs.io/en/)  
[Supertest](https://www.npmjs.com/package/supertest)  
