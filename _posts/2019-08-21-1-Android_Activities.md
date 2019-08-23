---
title:  "Andorid Activities"
excerpt: "안드로이드 액티비티"

categories:
  - Android

last_modified_at: 2019-08-21T18:30:00
---

- 사용자와 상호작용할 수 있는 화면 제공
- 액티비티마다 창이 하나씩 주어져 사용자 인터페이스를 끌어올 수 있음
- 일반적으로 화면을 가득 채우지만, 작은 창으로 만들어 다른 창 위에 띄울 수 있음
- 앱은 여러 개의 액티비티가 느슨하게 묶여있는 형태로 구성
- 새로운 액티비티를 시작하면 이전 액티비티는 스택에 보존(Back stack)
- 한 액티비티가 새로운 액티비티의 시작으로 중단된 경우, 액티비티의 **수명 주기 콜백 메서드**를 통해 알려짐

## Managing activity lifecycle
- Resumed : 액티비티가 화면 foreground에 있고 사용자 포커스를 갖고 있음
- Paused : 다른 액티비티가 foreground에 있지만, 이 액티비티도 여전히 표시되어 있음. 완전히 화면 안 덮은 상태
- Stopped : 다른 액티비티에 완전히 가려진 상태

```java
public class ExampleActivity extends Activity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // The activity is being created.
    }
    @Override
    protected void onStart() {
        super.onStart();
        // The activity is about to become visible.
    }
    @Override
    protected void onResume() {
        super.onResume();
        // The activity has become visible (it is now "resumed").
    }
    @Override
    protected void onPause() {
        super.onPause();
        // Another activity is taking focus (this activity is about to be "paused").
    }
    @Override
    protected void onStop() {
        super.onStop();
        // The activity is no longer visible (it is now "stopped")
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        // The activity is about to be destroyed.
    }
}
```

![activity_lifcycle](/assets/images/posts/190821/activity_lifecycle.png)

----
**ref :**  
[android developer docs - Activity lifecycle](https://developer.android.com/guide/components/activities.html)  

