---
title:  "[ROS-Unity] ROS와 Unity의 통신"
excerpt: "ROS와 다른 플랫폼간 통신"

categories:
  - ROS
  - Unity

last_modified_at: 2020-02-05T18:30:00
---

- **리눅스 기반 ROS**와 **윈도우 기반 Unity**간 통신은 어떻게 이루어지나?
- ROS에서 다른 플랫폼과의 **Topic Pub/Sub** 구현

### Requirements
- ROS : Web Socket 기반 rosbridge_suite 라이브러리
- Unity : rosbridge_client를 제공하는 ROS# 라이브러리

### ROS
- `sudo apt-get install ros-<rosdistro>-rosbridge-server` ros bridge 설치
- `roslaunch rosbridge_server rosbridge_websocket.launch` ros bridge 실행 (마스터 노드 구동 중)
- WebSocket on port 9090 by default
- `rostopic echo /cmd_vel` 해당 토픽(/cmd_vel)에 값을 echo

### Unity
- Assets에서 ROS# 설치
- GameObject에 RosConnector 스크립트 컴포넌트 추가
- WebSocket 연결할 url 지정 (ex. ws://192.168.1.2:9090)
- GameObject에 Topic publishing할 스크립트 컴포넌트 추가
![Unity Ros Connector](/assets/images/posts/200205/unity_rc.png)

### work flow
![Work Flow](/assets/images/posts/200205/workflow.png)
1. ROS bridge로 server-client WebSocket connection
2. 각각의 플랫폼에서 publisher/subscriber 등록

| ![example clips](/assets/images/posts/200205/ros_unity1.gif) |
|:--:|
| *ROS - Unity connection using ros bridge based on websocket*
캐릭터의 linear velocity, angular velocity를 unity에서 publish하는 예제 |

> P.S. [roslibjs](https://github.com/RobotWebTools/roslibjs)  
> 웹 기반 ROS 라이브러리도 존재  
> 조금 더 간단하게 접근할 수 있고, 이해하기 쉬웠음

----
**ref**  
[rosbridge suite (ros wiki)](http://wiki.ros.org/rosbridge_suite)  
[ros sharp](https://github.com/siemens/ros-sharp)