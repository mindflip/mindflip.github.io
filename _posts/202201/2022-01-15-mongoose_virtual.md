---
title: "[Node.js] mongoose virtual"
excerpt: "mongodb 내에 저장되지 않는 가상 프로퍼티"

categories:
  - Node.js
  - mongoose

last_modified_at: 2022-01-16T15:00:00
---

### Virtuals

- MongoDB에 저장되지 않고 사용할 수 있는 가상 프로퍼티
- 주로 document에서 computed properties로 사용
- db에 저장되지 않아 직접 쿼리를 이용해 조회하는 것은 불가

### simple example

```js
userSchema.virtual("domain").get(function () {
  return this.email.slice(this.email.indexOf("@") + 1);
});
```

- domain이란 가상의 프로퍼티를 만들기
- email 프로퍼티에서 @ 이후의 string을 가져오기
- 위의 schema로 생성된 model에서 `.domain`을 사용해 접근

### Virtuals in JSON

- json으로 컨버팅될 때 virtual은 default가 아님
- express js에서 `res.json()`을 사용할 때 json으로 컨버팅 되는데, 그때 virtual도 함께 가져오고 싶을 때 사용
- model을 정의할 때, `toJSON: { virtuals: true }` 포함

### Populate

- 다른 연관된 collection의 데이터를 사용하기 위해 사용
- populate을 정의하기 위해 아래 항목 사용
  - `ref` option : 어떤 모델이 document에 의해 populate 되는지 알려줌
  - `localField`, `foreignField` : foreignField와 해당 document의 localField가 일치하는 ref의 모델로부터 documents를 populate

```js
blogPostSchema.virtual("author", {
  ref: "User",
  localField: "authorId",
  foreignField: "_id",
  justOne: true,
});

const doc = await BlogPost.findOne().populate("author");
```

---

**ref :**  
[Mongoose Virtuals](https://mongoosejs.com/docs/tutorials/virtuals.html){:target="\_blank"}
