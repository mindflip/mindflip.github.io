---
title:  "[Docker] Container Images"
excerpt: "도커 이미지는 어디서 받아오고, 어떻게 빌드하나?"

categories:
  - Docker

last_modified_at: 2020-01-31T19:00:00
---

### 이미지란 무엇인가?
- 앱 바이너리 파일
- 컨테이너 런타임동안 root filesystem 변화의 컬렉션과 실행 파라미터
- 완전한 OS, kernel이 아님
- ex) golang 같은 static binary / Ubuntu (+apt, apache, php)

### 이미지 생성과 저장
- Dockerfile을 이용한 생성
- 도커 엔진 이미지 캐시에 저장
- 이미지 캐시에서 docker hub로 push / pull

### 이미지와 레이어
- 이미지는 파일 시스템 변화의 과정, 메타데이터를 모두 포함
- 각 레이어는 uniquely identified 되어있고 호스트에 한 번 저장
- 호스트의 저장 공간 확보 및 push/pull 시간 단축
- 컨테이너는 이미지 최상위의 read/write 레이어
- history, inspect 명령어를 이용해 layer 확인

### 이미지 태그와 ID
- 이미지 구분 : \<user>/\<repo>:\<tag>
- official repository는 root namespace로서 account name 필요 없음
- 이미지 ID는 이미지의 고유한 값
- 태그는 특정 이미지 ID를 지칭하는 단순 label / 같은 ID를 지칭하는 여러 개의 태그가 존재할 수도 있음

### Dockerfile
- 이미지를 구체화할 명세서
- 간단하게 명령어 정리
```bash
FROM (base image)  
ENV (environment variable)  
RUN (any arbitrary shell command)  
EXPOSE (open port from container to virtual network) • CMD (command to run when container starts)  
docker image build (create image from Dockerfile)  
```


----
**ref**  
[만들면서 이해하는 도커(Docker) 이미지의 구조](https://www.44bits.io/ko/post/how-docker-image-work)  