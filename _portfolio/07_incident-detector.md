---
title: "돌발검지 시뮬레이터"
excerpt: "RSU와 연동한 지도기반 돌발검지 시뮬레이터"
header:
  image: /assets/images/portfolio7/0.png
  teaser: /assets/images/portfolio7/th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio7/arch.png
    image_alt: "architecture"
    text: "Express.js"
  - title: "Used Skills"
    text: "Node.js (javascript)"
gallery:
  - image_path: assets/images/portfolio7/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio7/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio7/3.png
    alt: "app image 3"
---

{% include gallery caption="돌발검지 시뮬레이터 앱 스크린샷" %}

- 실제 돌발검지기가 하는 역할을 시뮬레이션
- 특정 구간을 설정 후, 구간을 이동하는 가상의 차량들과 돌발상황을 설정
- 차량/돌발상황에 관한 정보를 RSU에 TCP 전송

----

- 지도 : [Openlayers 오픈소스](https://openlayers.org/) 사용
- TCP connection : node.js net module 사용
- express.js 이용하여 웹기반 앱 구축
- RSU 인터페이스에 맞게 프로토콜 설계
- RSU를 대신할 test tcp server 구축
