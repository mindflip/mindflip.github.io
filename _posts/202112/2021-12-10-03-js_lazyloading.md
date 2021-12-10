---
title: "[Javascript] Lazy loading images"
excerpt: "웹성능 최적화를 위한 기법"

categories:
  - Javascript

last_modified_at: 2021-12-10T11:00:00
---

### Lazy loading

- 사용자가 특정 페이지에 접근할 때, 화면에 보이지 않는(사용하지도 않을 수 있는) 리소스까지 모두 로딩한다면 리소스 낭비로 이어질 수 있음
- 웹 성능, 디바이스 내 리소스 활용도 증가, 연관된 비용 줄이는 데 도움
- 사용자 화면에 보여질 필요가 있을 때까지 로딩을 지연하는 것
- 다양한 방법이 있지만 이 포스팅에서는 `IntersectionObserver API` 이용하여 구현

```html
<img
  src="img/grow-lazy.jpg"
  data-src="img/grow.jpg"
  alt="Plant"
  class="features__img lazy-img"
/>
```

```js
const imgTargets = document.querySelectorAll("img[data-src]");

const loadImg = function (entries, observer) {
  const [entry] = entries;

  if (!entry.isIntersecting) return;

  // Replace src with data-src
  entry.target.src = entry.target.dataset.src;

  entry.target.addEventListener("load", function () {
    entry.target.classList.remove("lazy-img");
  });

  observer.unobserve(entry.target);
};

const imgObserver = new IntersectionObserver(loadImg, {
  root: null,
  threshold: 0,
  rootMargin: "200px",
});

imgTargets.forEach((img) => imgObserver.observe(img));
```

- `IntersectionObserver API`는 사용자가 해당 구간에 intersection 하였는지 확인하는 역할
- 파라미터로 function, option 필요
- function은 api를 연결한 taget과 observer를 파라미터로 받음
- img는 낮은 해상도를 연결해놓고 사용자가 필요할 때 data-src에 저장해놓은 원본 화면을 보여주는 방식

---

**ref :**  
[intersection observer MDN](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API){:target="\_blank"}
