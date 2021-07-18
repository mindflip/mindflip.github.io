---
title: "학생 숙제관리 시스템"
excerpt: "학생들의 숙제 점수를 매기고, 현황을 그래프로 체크"
header:
  image: /assets/images/portfolio8/0.png
  teaser: /assets/images/portfolio8/th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio8/arch.png
    image_alt: "architecture"
    text: "Express.js, MongoDB"
  - title: "Used Skills"
    text: "Node.js (javascript)"
gallery:
  - image_path: assets/images/portfolio8/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio8/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio8/3.png
    alt: "app image 3"
---

{% include gallery caption="숙제관리 앱 스크린샷" %}

- 학생들의 숙제 현황 체크
- 학생들의 숙제 점수 관리
- 한 주 숙제를 모두 수행한 학생들은 숙제왕 타이틀 수여

----

- epress.js 기반 웹앱 구축
- MongoDB 이용하여 숙제, 학생, 학생점수 등 데이터 관리
- Mongoose 모듈 사용하여 DB와 통신
- 선생님 인증을 위한 passport 모듈 사용
- EJS 이용한 프론트엔드 구현
- chart.js 이용한 학생 점수 시각화
