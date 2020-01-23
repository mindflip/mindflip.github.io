---
title:  "[ROS] ROS Communication"
excerpt: "ROS 통신 방식"

categories:
  - ROS

last_modified_at: 2020-01-23T18:30:00
---

| ![ROS graph concept](/assets/images/posts/200123/graph_concept.png) |
|:--:|
| *ROS graph concepts. (a) Core computation graph level, (b) messages publish and subscribe communication between nodes to topics, (c) service request and response communication between server and client, (d) action communication between server and client.* |

### Topics (Ansyc / Unidir)
- 연속적인 데이터 스트림을 위해 사용 (sensor data, robot state, ...)
- 데이터는 발행과 구독될 수 있음
- Many to Many connection
- 데이터가 사용 가능할 때 callback / publisher가 데이터 보내는 것을 결정

### Services (Sync / Bi-dir)
- 요청에 응답하고 바로 종료되는 통신
- 프로세스가 길게 동작하지 않음
- 요구되는 데이터를 빠르게 처리할 때 사용

### Actions (Async / Bi-dir)
- 요청에 긴 시간에 걸쳐 응답하는 경우 사용
- 오랜시간 움직이는 로봇의 불연속적인 움직임에 사용, 피드백은 실행중에도 받음
- goal의 lifetime 동안은 상태를 유지
- 시작과 종료에 수 초가 걸리는 slow perception routines에 사용
- 현실 세계의 행동과 비슷함


----
**ref**  
[Topics vs Services vs Actionlib...](http://wiki.ros.org/ROS/Patterns/Communication)  
[ROS Terminology](https://robinrobotic.blogspot.com/2019/06/ros-terminology.html)  
[actionlib](http://wiki.ros.org/actionlib)  