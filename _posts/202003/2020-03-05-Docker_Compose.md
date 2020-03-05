---
title:  "[Docker] Docker Compose : The Multi-Container Tool"
excerpt: "Multi Container를 관리하는 기술"

categories:
  - Docker

last_modified_at: 2020-03-05T18:30:00
---

- 컨테이너들의 관계를 구성하기 위해 사용(멀티 컨테이너 관리)
- Container Run setting을 보기 쉽게 작성
- 환경설정 한 줄에 간략히 제공 가능
- 크게 2 가지로 구성
  - YAML : 다양한 옵션의 상세 정보 (containers, networks, volumes)
  - CLI tool docker-compose : 로컬에서 YAML을 이용하여 개발/테스팅 자동화

### docker-compose.yml
- versions : 1, 2, 2.1, 3, 3.1 등
- docker-compose 명령어를 통해 로컬에서 YAML 실행
- docker-compose --help 명령어로 사용법 이해

```yaml
version: '3.1'  # if no version is specificed then v1 is assumed. Recommend v2 minimum

services:  # containers. same as docker run
  servicename: # a friendly name. this is also DNS name inside network
    image: # Optional if you use build: (build 사용 시 image 이름 설정)
    command: # Optional, replace the default CMD specified by the image
    environment: # Optional, same as -e in docker run (항목들 list 또는 key-value 값으로 설정 가능)
    volumes: # Optional, same as -v in docker run
  servicename2:

volumes: # Optional, same as docker volume create

networks: # Optional, same as docker network create
```

### Sample one (Web with 3DBs)
```yaml
version: '3'

services:
  ghost:
    image: ghost
    ports:
      - "80:2368"
    environment:
      - URL=http://localhost
      - NODE_ENV=production
      - MYSQL_HOST=mysql-primary
      - MYSQL_PASSWORD=mypass
      - MYSQL_DATABASE=ghost
    volumes:
      - ./config.js:/var/lib/ghost/config.js
    depends_on:
      - mysql-primary
      - mysql-secondary
  proxysql:
    image: percona/proxysql
    environment: 
      - CLUSTER_NAME=mycluster
      - CLUSTER_JOIN=mysql-primary,mysql-secondary
      - MYSQL_ROOT_PASSWORD=mypass
   
      - MYSQL_PROXY_USER=proxyuser
      - MYSQL_PROXY_PASSWORD=s3cret
  mysql-primary:
    image: percona/percona-xtradb-cluster:5.7
    environment: 
      - CLUSTER_NAME=mycluster
      - MYSQL_ROOT_PASSWORD=mypass
      - MYSQL_DATABASE=ghost
      - MYSQL_PROXY_USER=proxyuser
      - MYSQL_PROXY_PASSWORD=s3cret
  mysql-secondary:
    image: percona/percona-xtradb-cluster:5.7
    environment: 
      - CLUSTER_NAME=mycluster
      - MYSQL_ROOT_PASSWORD=mypass
   
      - CLUSTER_JOIN=mysql-primary
      - MYSQL_PROXY_USER=proxyuser
      - MYSQL_PROXY_PASSWORD=s3cret
    depends_on:
      - mysql-primary
```

### docker-compose CLI
- 배포단계(production-grade)가 아닌 로컬 개발/테스팅에 적합
- 가장 자주 쓰는 두 명령어
  - `docker-compose up` : setup volumes/networks and start all containers
  - `docker-compose down` : stop all containers and remove cont/vol/net

### Using Compose to Build
- compose를 이용해 커스텀 이미지 빌드 가능
- `docker-compose up` 명령어 이용
- rebuild 명령어 `docker-compose build`
- image (key) 를 이용해 image name 설정 할 수 있음

----
**ref**  
[Compose file version 3 reference](https://docs.docker.com/compose/compose-file/#compose-and-docker-compatibility-matrix)  