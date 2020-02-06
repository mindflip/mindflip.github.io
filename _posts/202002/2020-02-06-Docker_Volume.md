---
title:  "[Docker] Container lifetime : Volumes"
excerpt: "컨테이너에서 생산되는 데이터를 관리하는 Volume"

categories:
  - Docker

last_modified_at: 2020-02-06T19:30:00
---

- 이미지는 read-only  
-> 컨테이너에 저장되는 데이터는 컨테이너가 삭제되면 함께 삭제
- 데이터를 영속적으로 사용할 수 있는 방법 : **Volume**

### Persistent data: Data Volumes
- 이미지 도커파일에 VOLUMES 정의된 경우, 데이터가 영구적으로 저장될 경로 생성 및 지정
- Image inspect 로 volume 경로 확인 가능
- 이미 생성된 volume 경로로 이미지 생성 가능
- Volume ls 이용하여 이제까지 생성된 volume 확인 가능
- Container stop 해도 volume 존재
- run에서 -v command 이용하여 경로지정 또는 v_name:/dir/dir 형식으로 네이밍
- docker volume create 이용하여 따로 volume 을 생성할 수도 있음

### Persistent Data: Bind Mounting
- Bind mounting : 호스트 파일/경로를 컨테이너 파일/경로에 매핑
- 두 경로가 하나의 물리적 하드의 경로를 가리킴(?)
- 호스트 파일이 컨테이너의 파일을 overwrite
- Dockerfile에서 사용 불가, container run 런타임 명령어에서만 사용  
ex) run -v /Users/pne/stuff:/path/container (max/linux)  
colon 왼쪽엔 full path 명시  
bind mount는 naming과 다르게 forward slash로 시작  
colon 오른쪽엔 호스트로부터 컨테이너에 매핑하고 싶은 디렉토리 명시
- 호스트에서 사용하는 파일에 접근하는 컨테이너에서 서비스 러닝할 때 필요  
서버 로그를 확인한다거나 할 때, 컨테이너에 접근할 필요 없이 로컬에 바인딩된 폴더/파일로 바로 접근 가능

----
**ref**  
[Docker 정리 #3 (도커 볼륨)](https://jungwoon.github.io/docker/2019/01/13/Docker-3/)  