---
title: "[Javascript] defer and async script loading"
excerpt: "html에 script를 로딩하는 방식"

categories:
  - Javascript

last_modified_at: 2021-12-10T11:30:00
---

### Defer and Async script loading

|         |                                  HEAD                                  |                           BODY END |
| :------ | :--------------------------------------------------------------------: | ---------------------------------: |
| REGULAR |         HTML 파싱 도중에 scipt fetch, execute, 이후 다시 파싱          | HTML 파싱 후 script fetch, execute |
| ASYNC   | scipt를 만나면 HTML 파싱 동시에, execute 시 파싱 잠시 멈추고 다시 파싱 |                     makes no sense |
| DEFER   |           HTML 파싱 도중에 script fetch, 파싱 끝나면 execute           |                     makes no sense |

```html
<script src="script.js">
<script async src="script.js">
<script defer src="script.js">
```

- defer이 전반적으로 최적의 구동방식
- defer는 `DOMContentLoaded` 직전에 실행 마침

---

**ref :**  
[Scripts: async, defer](https://javascript.info/script-async-defer){:target="\_blank"}
