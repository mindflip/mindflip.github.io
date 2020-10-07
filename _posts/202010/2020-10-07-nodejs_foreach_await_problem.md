---
title:  "[Node.js] foreach await problem"
excerpt: "async 함수가 foreach에는 영향이 없다!?"

categories:
  - Javascript
  - Node.js

last_modified_at: 2020-10-07T18:00:00
---

### 데이터가 화면에 안 떠요
- 웹상에서 필요한 데이터가 어떨 때는 뜨고, 어떨 때는 안 뜸
- 프론트엔드에는 문제가 없음
- 백엔드에서 데이터 불러오는 문제

### async await이 적용되지 않는 메서드!?
- 코드상에서 여러 model을 get하여 데이터를 연동해주는 작업이 필요
- array로 받아오기 때문에 forEach를 사용해 element 순회
- 그런데 forEach 내부에서 await 기능이 제대로 동작하지 않음

```js
exports.getHomeworkScoreByHomeworkGroupId = async (req, res, next) => {
...
    homework.forEach( async (element) => {
        const homeworkScore = await homeworkScoreModel.find({ homework_id: element._id });
        // console.log(homeworkScore);
        aryHomeworkScore = aryHomeworkScore.concat(homeworkScore);
    });
...
}
```

### 어떻게 해결하나?
- forEach를 for of 문으로 수정하니 await 이 적용됨

```js
for(const element of homework) {
    const homeworkScore = await homeworkScoreModel.find({ homework_id: element._id });
    aryHomeworkScore = aryHomeworkScore.concat(homeworkScore);
}
```

### 분석
- async / await 함수는 generator function으로 동작
- forEach는 각 iteration이 generator function으로 동작하여, 다른 generator와 독립적으로 수행
- for()이나 for of는 single generator function으로 동작하여 await 적용

----
**ref :**  
[Using async/await with a forEach loop](https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop)  
