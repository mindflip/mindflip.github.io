---
title: "쿨링글러브 App"
excerpt: "펠티어 모듈을 장착한 글러브를 Bluetooth UART 통신을 이용해 온도 제어"
header:
  image: /assets/images/portfolio1/0-mod.png
  teaser: /assets/images/portfolio1/0-mod-th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio1/arch.png
    image_alt: "architecture"
    text: "Android + WAMP STACK"
  - title: "Used Skills"
    text: "JAVA, PHP, MYSQL"
gallery:
  - image_path: assets/images/portfolio1/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio1/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio1/3.png
    alt: "app image 3"
  - image_path: assets/images/portfolio1/4.png
    alt: "app image 4"
  - image_path: assets/images/portfolio1/5.png
    alt: "app image 5"
  - image_path: assets/images/portfolio1/6.png
    alt: "app image 6"
---

- 과제명 : 사물인터넷 기반 운동 능력 향상을 위한 스마트 쿨링 글러브 시스템 개발 (문화체육관광부R&D)

{% include gallery caption="Glove S 앱 스크린샷" %}

- 블루투스 통신을 이용한 펠티어 온도 조절 및 생체정보 저장 어플리케이션
- 측정된 온도 및 심박 데이터는 어플리케이션을 통해 서버에 저장

-----

- 블루투스 페어링 후 GATT 프로토콜을 이용한 UART 방식으로 송수신
  - Tx, Rx에 대한 특정 UUID 값이 존재 (control device 기준의 Tx, Rx)

- UARTService 클래스를 이용하여 앱이 백그라운드인 상태에서도 BT연결 유지 및 데이터 수신
- BroadcastReceiver 를 MainActivity, UARTService 에 선언한 후 BT 데이터 전송
  - Service 클래스에서 BR을 선언하여 앱을 완전히 종료하지 않았을 경우에는 계속해서 Data를 받았다고 Broadcast 를 해준다
  - MainActivity에서는 그 값을 받아 (BR 의 onReceive 메서드) 다양하게 처리 (UI 업데이트, 서버 전송 등)

- PHP 로 개발한 서버를 통해 사용자 및 생체정보 저장