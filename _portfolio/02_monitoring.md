---
title: "공정모니터링 App"
excerpt: "자동화 장비의 오류 감지 및 모니터링 시스템"
header:
  image: /assets/images/portfolio2/0.png
  teaser: /assets/images/portfolio2/0.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio2/arch.png
    image_alt: "architecture"
    text: "Android + Arduino IP Cam, wifi + Node.js"
  - title: "Used Skills"
    text: "JAVA, Node.js, Firebase"
gallery:
  - image_path: assets/images/portfolio2/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio2/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio2/3.png
    alt: "app image 3"
  - image_path: assets/images/portfolio2/4.png
    alt: "app image 4"
  - image_path: assets/images/portfolio2/5.png
    alt: "app image 5"
  - image_path: assets/images/portfolio2/6.png
    alt: "app image 6"
---

- 과제명 : 50% 이상 공정시간 단축 및 저전압 효율 특성을 가진 마그네슘 및 알루미늄 합금에 혼용 가능한 지능형 플라즈마 전해 산화 표면처리 장비 개발 (산업통상자원부)

{% include gallery caption="Monitoring 앱 스크린샷" %}

- WebView를 이용해 공장에 설치한 Arduino 기반 IP Camera 스트리밍
- 오류상황 감지를 위한 아두이노 센서 설치
- 오류상황에 App에 Push 메시지 전송
- 카메라 IP setting 및 산화피막 형성률 계산

----

- 푸쉬메시지는 Google Firebase 의 Cloud Messaging (FCM) 이용하여 Node.js 서버 구현
- 오류감지센서(Arduino+wifi module)가 특정 값을 받았을 경우 서버에 푸쉬 요청 