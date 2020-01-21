---
title:  "[Docker] Docker Introduction"
excerpt: "도커는 무엇이며, 사용하는 이유"

categories:
  - Docker

last_modified_at: 2020-01-02T19:00:00
---

![docker](/assets/images/posts/200102/docker_icon.png){:height="250px" width="250px"}

## Docker
- 컨테이너 기반의 오픈소스 가상화 플랫폼
- 다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공해 배포/관리 단순화

## Container
- 격리된 공간에서 프로세스가 동작하는 기술
- 가상화 기술의 하나이지만 VM과는 다름 [[참고](https://goto.docker.com/rs/929-FJL-178/images/docker-for-the-virtualization-admin.pdf)]

## Image
- 컨테이너 실행에 필요한 파일과 설정을 포함
- ex) ubuntu, mysql, nginx
- [Docker hub](https://hub.docker.com/search?q=&type=image) 에서 이미지를 받아와 설치

### 도커를 사용하는 이유
- 환경에 독립적이어서 앱을 실행하기 편리하고 확장성 우수
- 서버를 코드로 구성하고 관리 (Docker file)
- 언제든 똑같은 형태의 서버를 실행 가능

### 서버 코드화의 장점
- 서버 제작 과정에 견고함과 유연성 제공
- 다른 이가 만든 서버를 소프트웨어 사용하듯 가져다 사용
- 여러 대에 배포할 수 있는 확장성

>도커 파일 == 서버 운영 기록  
도커 이미지 == 도커 파일 + 실행 시점  
도커 컨테이너 == 도커 이미지 + 환경 변수


----
**ref :**  
- [왜 굳이 도커(컨테이너)를 써야 하나요?](https://www.44bits.io/ko/post/why-should-i-use-docker-container)  
- [초보를 위한 도커 안내서 - 도커란 무엇인가?](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)