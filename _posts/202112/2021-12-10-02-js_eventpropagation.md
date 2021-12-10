---
title: "[Javascript] DOM and Event propagation"
excerpt: "이벤트가 전파되는 과정"

categories:
  - Javascript

last_modified_at: 2021-12-10T10:30:00
---

### DOM

- Document Object Model
- js와 브라우저와 상호작용을 가능하게 함
- js를 이용해서 HTML elements를 생성, 수정, 삭제 가능
- DOM tree는 HTML document에서 만들어짐
- DOM tree와 상호작용을 위해 다양한 메서드와 프로퍼티를 가진 상당히 복잡한 API

### Bubbling and Capturing

```html
<html>
  <body>
    <section>
      <p>This is example</p>
    </section>
  </body>
</html>

<!--
Capturing phase
Document -> Element<html> -> Element<body> -> Element<section> -> Element<p>

Bubbling phase
Element<p> -> Element<section> -> Element<body> -> Element<html> -> Document
-->
```

### Event delegation

- Event propagation을 이용하여 다양한 적용 가능
- ex) Nav bar에 각 메뉴들에 대한 click event를 적용하는 것이 아니라, nav bar 자체에 click 이벤트를 적용하여 각 메뉴를 클릭할 때를 catch
- 위와 같은 예제를 event delegation이라 함 (각각의 nav menu 대신 nav bar에 역할을 위임)
- 각 메뉴에 event handler를 생성하는 것은 상당한 오버헤드가 되기 때문에 event delegation 사용

```js
document.querySelector(".nav_links").addEventListener("click", function (e) {
  e.preventDefault();

  if (!e.target.classList.contains("nav_link")) return;
  const id = e.target.getAttribute("href");
  document.querySelector(id).scrollIntoView({ behavior: "smooth" });
});
```

---

**ref :**  
[bubbling capturing js info](https://javascript.info/bubbling-and-capturing){:target="\_blank"}
