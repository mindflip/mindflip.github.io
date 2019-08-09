---
title: "쿨링자켓 App"
excerpt: "펠티어 모듈을 장착한 자켓을 Bluetooth UART 통신을 이용해 온도 제어"
header:
  image: /assets/images/portfolio4/0.png
  teaser: /assets/images/portfolio4/th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio4/arch.png
    image_alt: "architecture"
    text: "Android"
  - title: "Used Skills"
    text: "JAVA"
gallery:
  - image_path: assets/images/portfolio4/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio4/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio4/3.png
    alt: "app image 3"
  - image_path: assets/images/portfolio4/4.png
    alt: "app image 4"
  - image_path: assets/images/portfolio4/5.png
    alt: "app image 5"
  - image_path: assets/images/portfolio4/6.png
    alt: "app image 6"
---

- 과제명 : 노인·근로자의 열피로 회복 및 고열장애 예방을 위한 스마트 쿨링 자켓 개발 (중소벤처기업부)

{% include gallery caption="Cooling Jacket 앱 스크린샷" %}

- 자켓 온도 조절을 위한 안드로이드 App 개발
- 온도 조절 모듈과 블루투스 통신 (UART)

----

- 블루투스 페어링 후 GATT 프로토콜을 이용한 UART 방식으로 송수신
  - Tx, Rx에 대한 특정 UUID 값이 존재 (control device 기준의 Tx, Rx)
- UARTService 클래스를 이용하여 앱을 활성화하지 않은 상태에서도 BT연결 유지 및 데이터 수신
