---
title: "농민사관학교 출석 시스템"
excerpt: "출석을 위해 위치 기반(QR code + GPS) 인증을 거치며 출석현황 확인, 강의 평가 등의 기능 수행"
header:
  image: /assets/images/portfolio5/0.png
  teaser: /assets/images/portfolio5/th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio5/arch.png
    image_alt: "architecture"
    text: "Android/iOS + Node.js + MSSQL"
  - title: "Used Skills"
    text: "JAVA, SWIFT, Node.js"
gallery:
  - image_path: assets/images/portfolio5/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio5/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio5/3.png
    alt: "app image 3"
  - image_path: assets/images/portfolio5/4.png
    alt: "app image 4"
  - image_path: assets/images/portfolio5/5.png
    alt: "app image 5"
  - image_path: assets/images/portfolio5/6.png
    alt: "app image 6"
  - image_path: assets/images/portfolio5/7.png
    alt: "app image 7"
---

{% include gallery caption="경북대학교 EMR 연동 앱 스크린샷" %}

- 출석을 위한 안드로이드, iOS App 개발
- App과 DB 연동을 위한 REST API 개발
- 출석, 강의평가를 위한 DB 설계
- Google play store, Apple app store 배포

----

- QR code, HTTP Client(Android : Retrofit, iOS : Alamofire) 외부 라이브러리 사용
- QR code에 수업 코드, 위치 정보가 입력되어 있어, QR을 인식하면 출석 인증에 대한 조건 처리 후 서버에 출석 요청
- 출석 현황, 수료한 수업 이력 등을 확인
- 부정출결 방지를 위해 모바일 단말의 uuid를 DB에 저장하여 타인의 단말기로 로그인하여 대리출석하는 것을 방지
