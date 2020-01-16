---
title:  "[Unity] Event Functions and Order of Execution"
excerpt: "이벤트 함수와 함수의 실행 순서"

categories:
  - Unity

last_modified_at: 2020-01-16T19:00:00
---

## Event Functions
- Unity는 스크립트 안에 선언된 특정 함수를 호출해 컨트롤을 간헐적으로 스크립트에 전달
- 함수 실행이 완료되면 컨트롤이 다시 Unity에 반환
- 게임 플레이 중 발생하는 이벤트에 응답으로 Unity에서 활성화되기 때문에 `이벤트 함수`라고 함
- ex) Update 함수(프레임 업데이트 전 호출) / Start 함수(오브젝트 첫 프렝미 업데이트 직전)
- 가장 많이 사용하는 이벤트 일부 소개

### Regular Update Events
- 각 프레임이 렌더링되기 전에 오브젝트 포지션, 상태 및 동작을 변경하는 것이 게임 프로그래밍 핵심
- **Update** 함수에서 주로 다루게 됨
- 프레임이 렌더링되기 전에 호출, 애니메이션 계산되기 전에도 호출
```c#
void Update() {
    float distance = speed * Time.deltaTime * Input.GetAxis("Horizontal");
    transform.Translate(Vector3.right * distance);
}
```

- **FixedUpdate**는 각 물리 업데이트 직전 호출
- 물리 업데이트와 프레임 업데이트는 동일한 빈도로 실행되지 않음
- 따라서 Update 대신 FixedUpdate 함수에 물리코드 삽입하여 더 정확한 결과 값 획득
```c#
void FixedUpdate() {
    Vector3 force = transform.forward * driveForce * Input.GetAxis("Vertical");
    rigidbody.AddForce(force);
}
```

- Scene의 모든 오브젝트에 대해 Update, FixedUpdate를 호출한 후와 모든 애니메이션이 계산된 후 변경 사항을 추가로 적용할 때 **LateUpdate** 함수 사용
- ex) 카메라가 타겟 오브젝트를 계속 트래킹할 때 : 타겟 오브젝트가 이동한 후 카메라 방향 조정
```c#
void LateUpdate() {
    Camera.main.transform.LookAt(target.transform);
}
```

### Initialization Events
- **Start** : 첫 프레임이나 오브젝트 물리 업데이트 전 호출
- **Awake** : 씬이 로드될 때 각 오브젝트에 대해 호출
- 다양한 오브젝트의 Start, Awake 함수는 임의로 호출되지만, 모든 Awake는 첫 Start가 호출되기 전에 완료
- Start는 Awake에 이미 수행된 다른 초기화를 이용

### GUI events
- Scene의 메인 액션 위에 GUI 컨트롤 렌더링, 컨트롤하는 시스템
- 일반 프레임 업데이트와 다르게 처리되므로, 주기적으로 호출되는 OnGUI 함수 이용
```c#
void OnGUI() {
    GUI.Label(labelRect, "Game Over");
}
```

### Physics events
- 물리 엔진은 오브젝트의 스크립트에 있는 이벤트 함수 호출해 오브젝트 충돌 보고
- `OnCollisionEnter`, `OnCollisionStay`, `OnCollisionExit` 함수는 접촉 발생, 유지, 분리될 때 호출
- `OnTriggerEnter`, `OnTriggerStay`, `OnTriggerExit` 함수는 오브젝트 콜라이더가 트리거(물리적 반응X 감지O)로 설정된 경우에 호출
```c#
void OnCollisionEnter(otherObj: Collision) {
    if (otherObj.tag == "Arrow") {
        ApplyDamage(10);
    }
}
```

----
## Order of Execution for Event Functions
![monobehaviour flowchart](/assets/images/posts/200116/monobehaviour_flowchart.png)
- 그림 설명은 ref 참고



----
**ref**  
[Event Functions(Unity Doc)](https://docs.unity3d.com/2020.1/Documentation/Manual/EventFunctions.html)  
[Order of Execution for Event Functions(Unity Doc)](https://docs.unity3d.com/2020.1/Documentation/Manual/ExecutionOrder.html) 
