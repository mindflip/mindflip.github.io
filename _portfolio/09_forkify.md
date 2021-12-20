---
title: "레시피 검색 페이지"
excerpt: "레시피를 찾기 및 업로드를 할 수 있는 프론트 페이지"
header:
  image: /assets/images/portfolio9/0.png
  teaser: /assets/images/portfolio9/th.png
sidebar:
  - title: " "
    image: /assets/images/portfolio9/arch.png
    image_alt: "architecture"
    text: " "
  - title: "Used Skills"
    text: "vanilla javascript"
gallery:
  - image_path: assets/images/portfolio9/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio9/2.png
    alt: "app image 2"
---

{% include gallery caption="레시피 검색 및 업로드" %}

- 레시피 검색하여 확인, 인원 수에 따른 재료 양 확인
- 즐겨찾기 추가 및 삭제
- 레시피 업로드

---

- MVC 패턴 기반 프론트엔드 개발
- Model
  - 레시피 불러오기, 검색 결과 등의 데이터를 다루는 모듈 구현
  - fetch API를 이용해서 백엔드에 요청
- View
  - render, update, error 등을 처리하는 View.js 구현 후, 대부분의 모듈에서 상속하여 사용
  - 모듈화하여 컴포넌트 사용성 증가
- Controller
  - Model과 View를 연결해주는 컨트롤러 모듈 구현
  - UI에서 발생한 이벤트를 model에 전달해주어 데이터 처리

### [Github repo](https://github.com/mindflip/forkify){:target="\_blank"}

### [DEMO APP](https://forkify-mindflip.netlify.app/){:target="\_blank"}
