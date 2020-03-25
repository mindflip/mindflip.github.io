---
title:  "[ROS] Recording and playing back data (rosbag)"
excerpt: "ROS 데이터 기록 및 재생"

categories:
  - ROS

last_modified_at: 2020-03-24T18:30:00
---

- 계속해서 갱신되는 Topic 데이터를 기록하고, 후에 분석을 위해 다시 재생하고 싶을 때 `rosbag` 명령어 사용

### Recording data (creating a bag file)
- `roscore` 및 topic node 실행
- `rostopic list -v` 이용하여 pub / sub topics 확인
- `rosbag record -a` 특정 폴더 만들어 명령어 실행
  - -a : 모든 토픽에 대해 recording
  - Ctrl+C로 recording 중지하면, 해당 디렉토리에 year, date, and time 으로 조합된 이름의 .bag 파일 생성

### Examining and playing the bag file
- `rosbag info <your bagfile>` 이용하여 bag 파일 정보 확인
  - 기록된 시간, 메시지 수, topic 종류 등
- `rosbag play <your bagfile>` 이용하여 bag 파일 재생
  - `rosbag play -r 2 <your bagfile>` -r 옵션으로 rate 조절 가능

### Recording a subset of the data
- `rosbag record -O subset /cmd_vel`
  - -O : 특정 파일 네임으로 저장. 여기선 subset
  - 특정 토픽에 대해서만 저장. 여기선 /cmd_vel

### The limitations of rosbag record/play
- 값을 기록한 뒤 다시 노드에서 재생시켜보면, 아주 정확하지는 않음
- 실제 노드에서 publish하는 동작들은 작은 변화에도 매우 sensitive하여, 기록에 한계가 있음

----
**ref**  
[Recording and playing back data](http://wiki.ros.org/rosbag/Tutorials/Recording%20and%20playing%20back%20data)  