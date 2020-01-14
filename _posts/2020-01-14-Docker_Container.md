---
title:  "[Docker] Container command"
excerpt: "컨테이너 사용법, 명령어"

categories:
  - Docker

last_modified_at: 2020-01-14T19:00:00
---

```bash
docker version    // verified cli can talk to engine  
docker info       // most config values of engine
```

### Docker command line structure
- old (still work) : docker \<command> (options)
- new : docker \<command> \<sub-command> (options)

### Image vs. Container
- 이미지는 실행시키고 싶은 어플리케이션
- 컨테이너는 프로세스로 실행되는 이미지 인스턴스
- 같은 이미지를 이용해 많은 컨테이너 실행 가능

```bash
docker containerr run --publish 80:80 nginx  
// nginx를 Docker hub에서 다운로드
// 이미지를 이용해 컨테이너 실행
// host ip 에서 80 포트 사용
// contianer ip 에서 80 포트 사용
```

### docker container run 명령어가 하는 일
- 이미지 캐시에서 이미지 찾기
- 캐시에서 못 찾으면, 이미지 repository (default to Docker hub)에서 찾기
- 버전 지정 안 할 시 최신 버전으로 이미지 다운
- 이미지를 기반으로 새로운 컨테이너 생성
- 도커 엔진의 private network에 가상 ip 제공
- host에서 80포트 개방, 컨테이너에서 80포트 포워딩
- image Dockerfile의 명령어로 컨테이너 실행

```bash
docker container top        // process list in one container  
docker container inspect    // details of one container configg
docker container stats      // performance stats for all containers

docker container run -it    // start new container interactively
docker container exec -it   // run additional command in existing container
```

--------
### Docker Networks Defaults
- 각 컨테이너는 private virtual network "bridge"에 연결됨
- 각 가상 네트워크는 호스트 IP의 NAT 방화벽을 이용해 라우팅
- 가상 네트워크의 모든 컨테이너는 -p 없이 서로 통신 가능
- 가장 좋은 방식은 각 앱마다 새로운 가상 네트워크 생성
  - network "my_web_app" for mysql and php/apache containers
  - network "my_api" for mongo and nodejs containers

### CLI Management
```bash
docker network ls                 // Show networks
docker network inspect            // Inspect a network
docker network create --driver    // Create a network
docker network connect            // Attach a network to container
docker network disconnect         // Detach a network from container
```

### Docker networks: DNS
- DNS는 이컨테이너 끼리의 inter-communication을 이해하는 것
- 컨테이너는 inter-communication을 위해 IP 응답을 하지 않음

```bash
docker container exec -it my_nginx ping new_nginx  
// IP를 따로 이용하지 않고 name setting으로 ping 통신
```