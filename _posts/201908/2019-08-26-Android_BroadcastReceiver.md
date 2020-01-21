---
title:  "[Andorid] Broadcast Receiver"
excerpt: "안드로이드 브로드캐스트 리시버"

categories:
  - Android

last_modified_at: 2019-08-26T18:30:00
---

- 시스템이나 앱에서 이벤트 발생 시 broadcast를 해주는데, broadcast receiver를 이용하여 이런 이벤트를 처리

## Receiving broadcasts

- 브로드 캐스트를 받는 두 가지 방법 : manifest-declared / context-registered

### Manifest-declared receivers

- Manifest에 `<receiver>` element 등록
  - intent filter로 구체적인 액션을 등록

```xml
<receiver android:name=".MyBroadcastReceiver"  android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="android.intent.action.INPUT_METHOD_CHANGED" />
    </intent-filter>
</receiver>
```

- 서브클래스 `BroadcastReceiver` 의 `onReceive(Context, Intent)` 구현
  - 밑의 예제는 브로드캐스트의 내용을 로깅해보는 것

```java
public class MyBroadcastReceiver extends BroadcastReceiver {
        private static final String TAG = "MyBroadcastReceiver";
        @Override
        public void onReceive(Context context, Intent intent) {
            StringBuilder sb = new StringBuilder();
            sb.append("Action: " + intent.getAction() + "\n");
            sb.append("URI: " + intent.toUri(Intent.URI_INTENT_SCHEME).toString() + "\n");
            String log = sb.toString();
            Log.d(TAG, log);
            Toast.makeText(context, log, Toast.LENGTH_LONG).show();
        }
    }
```

### Context-registered receivers

- `BroadcastReceiver` 인스턴스 생성

```java
BroadcastReceiver br = new MyBroadcastReceiver();
```

- `IntentFilter` 생성, `registerReceiver(BroadcastReceiver, IntentFilter)` 호출하여 리시버 등록

```java
IntentFilter filter = new IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION);
    filter.addAction(Intent.ACTION_AIRPLANE_MODE_CHANGED);
    this.registerReceiver(br, filter);
```

- Context-registered receivers 는 registering context가 유효한 경우만 broadcast receive
- ex) Activity에 등록을 했다면, Activity가 destroy되지 않는한 broadcast를 receive
- ex) Application context에 등록했다면 app이 실행중에는 항상 broadcast receive
- broadcast receive를 중단하고 싶다면 `unregisterReceiver(android.content.BroadcastReceiver)` 호출


## Sending broadcasts
안드로이드는 broadcast를 보내는 세 방법을 제공:
- `sendOrderedBroadcast(Intent, String)` 한 순간에 하나의 리시버에만 broacast
- `sendBroadcast(Intent)` 정해져있지 않은 순서로 모든 리시버에게 broadcast (Normal Broadcast)
- `LocalBroadcastManager.sendBroadcast` sender와 같은 앱에 있는 리시버에게 broadcast

```java
Intent intent = new Intent();
intent.setAction("com.example.broadcast.MY_NOTIFICATION");
intent.putExtra("data","Notice me senpai!");
sendBroadcast(intent);
```

- 브로드캐스트 메시지는 Intent 객체에 wrapped
- Intent 의 action 문자열은 java 패키지와 브로드캐스트 이벤트를 구분할 unique id를 제공해야 함
- `putExtra(String, Bundle)`을 사용해 추가적인 정보를 intent에 추가

----
**ref :**  
[android developer docs - Broadcast overview](https://developer.android.com/guide/components/broadcasts)

