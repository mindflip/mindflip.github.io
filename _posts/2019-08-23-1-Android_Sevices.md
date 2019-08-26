---
title:  "Andorid Services"
excerpt: "안드로이드 서비스"

categories:
  - Android

last_modified_at: 2019-08-23T18:30:00
---

- 백그라운드에서 오래 실행되는 작업을 수행할 수 있는 컴포넌트(인터페이스 X)
- 컴포넌트를 서비스에 바인드하여 서비스와 상호작용 가능, 프로세스 간 통신(IPC) 수행 가능

----
서비스의 두 가지 형식
- Started service
  - 컴포넌트가 `startService()` 호출하여 시작
  - 한 번 시작되면 백그라운드에서 무기한으로 실행 가능
  - 서비스를 시작한 컴포넌트의 소멸에 관계 없음
  - 작업이 완료되면 `stopSelf()`를 호출하여 스스로 알아서 중단하는 것이 정상, 아니면 다른 구성 요소가 `stopService()`를 호출하여 중단

- Bound service
  - 컴포넌트가 `bindService()` 호출하여 해당 서비스에 바인드(bind)
  - `onBind()` 콜백 메서드를 구현하여 서비스와의 통신을 위한 인터페이스를 정의하는 IBinder를 반환
  - client-server 인터페이스 제공하여 컴포넌트-서비스 상호작용
  - 클라이언트가 서비스와의 상호작용을 완료하면 이는 `unbindService()`를 호출하여 바인딩을 해제
  

컴포넌트가 서비스 시작 : `onStartCommand()`  
컴포넌트가 바인딩 허용 : `onBind()`

두 가지 의 큰 차이점은 서비스가 백그라운드에서 도는지(started) 다른 컴포넌트와 상호작용을 하는지(bound)의 여부:  
[check1](https://stackoverflow.com/questions/13787460/when-is-smart-to-use-bindservice-and-when-startservice) [check2](https://www.101apps.co.za/articles/binding-to-a-service-a-tutorial.html)  
ex) bound servive는 association/client/activity이 존재해야 사용가능. association 과 관계가 끊어지면 (종료하면) UI가 destroy되고 그것은 곳 bound service도 소멸되는 것. started service는 association의 destroy와 상관 없이 백그라운드에서 계속 실행됨. 서비스의 수행이 종료되면 자동 소멸.


## Managing the lifecycle of a service

![serviceLifecycle](/assets/images/posts/190823/service_lifecycle.png)
- 서비스의 전체 수명 주기 `onCreate()` ~ `onDestroy()`
- 서비스의 활성 수명 주기는 `onStartCommand()` 또는 `onBind()`에 대한 호출로 시작
  - 각 메서드에 Intent가 전달되며 이것은 각각 `startService()` 또는 `bindService()`에 전달된 것



----
**ref :**  
[android developer docs - Services overview](https://developer.android.com/guide/components/services)
[all about service](https://www.101apps.co.za/articles/all-about-services.html)
[started service vs bound service](https://stackoverflow.com/questions/13787460/when-is-smart-to-use-bindservice-and-when-startservice)

