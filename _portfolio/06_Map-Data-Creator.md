---
title: "Map Data Creator"
excerpt: "J2735 기반 Map Data Message 생성 프로그램"
header:
  image: /assets/images/portfolio6/0.png
  teaser: /assets/images/portfolio6/th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio6/arch.png
    image_alt: "architecture"
    text: ".NET Framework (Winform)"
  - title: "Used Skills"
    text: "C#"
gallery:
  - image_path: assets/images/portfolio6/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio6/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio6/3.png
    alt: "app image 3"
---

{% include gallery caption="Map Data Creator 앱 스크린샷" %}

- RSU에서 차량으로 송신할 Message인 Map Data 생성
- J2735(차량통신 메시지 표준)를 참고하여 Format 구성
- Winform 기반 G-map Nuget package를 이용하여 개발

----

- 마우스 위치 좌표 표시 및 좌표 입력으로 지도 표시
- Reference / Lane 노드 마킹
- 데이터 저장 및 불러오기
- Json, XML 형식으로 추출

### [To check specific manual](https://github.com/mindflip/Map-Data-Creator)