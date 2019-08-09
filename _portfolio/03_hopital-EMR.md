---
title: "병원EMR시스템 연동 App"
excerpt: "병원 내 EMR 시스템을 App과 연동하여 진료 예약, 진료 기록 확인 등의 활동을 장소의 제약 없이 수행"
header:
  image: /assets/images/portfolio3/0.png
  teaser: /assets/images/portfolio3/th.png
sidebar:
  - title: "Architecture"
    image: /assets/images/portfolio3/arch.png
    image_alt: "architecture"
    text: "Android + Relay Server"
  - title: "Used Skills"
    text: "JAVA, Node.js"
gallery:
  - image_path: assets/images/portfolio3/1.png
    alt: "app image 1"
  - image_path: assets/images/portfolio3/2.png
    alt: "app image 2"
  - image_path: assets/images/portfolio3/3.png
    alt: "app image 3"
  - image_path: assets/images/portfolio3/4.png
    alt: "app image 4"
  - image_path: assets/images/portfolio3/5.png
    alt: "app image 5"
  - image_path: assets/images/portfolio3/6.png
    alt: "app image 6"
---

- 과제명 : 실내 네비게이션 기반 맞춤형 의료정보 서비스 시스템 개발 (첨단정보통신융합산업기술원)

{% include gallery caption="경북대학교 EMR 연동 앱 스크린샷" %}

- REST API를 이용한 병원 EMR 시스템 연동
- 환자 진료, 원무 행정 등 대부분 정보를 요청 및 응답
- Node.js를 이용한 임시 Relay server 구축

----

- 안드로이드 App 에서 병원 EMR 서버 사이의 통신을 위해 Retrofit (HTTP Client Library) 사용
- Network 연결은 계속 유지시키기 때문에 Singleton pattern으로 구현
- 진료 예약, 진료 예약 확인, 사용자 정보 갱신 등 모든 요청을 query string을 이용하여 처리
- 응답은 XML 형식으로 받아와 simpleXML 라이브러리를 이용해 파싱

- 임시로 Node.js 를 이용해 릴레이 (Query string 그대로 다시 EMR 서버에 요청) 서버 구축
- 실제 DMZ 단에 들어가는 서버는 JAVA Tomcat 서버로 구현(다른 연구원이 개발)