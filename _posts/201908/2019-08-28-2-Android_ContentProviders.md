---
title:  "[Andorid] Content Providers"
excerpt: "안드로이드 컨텐트 프로바이더"

categories:
  - Android

last_modified_at: 2019-08-28T19:30:00
---

앱이 자체적으로 저장된 데이터, 다른 앱이 저장한 데이터에 대한 액세스 권한을 관리하도록 돕고 다른 앱과 데이터를 공유할 방법 제공

![cp](/assets/images/posts/190828/contentproviders_main.png)

### 특징
1. ContentResolver를 사용해 어플리케이션 사이의 data를 공유할 수 있음
2. ContentProvider를 구현한 어플리케이션의 data를 삽입, 삭제, 갱신, 조회 등의 작업 수행
3. ContentProvider를 구현한 어플리케이션은 실행중이 아니더라고 상대방에서 ContentProvider를 이용한 접근이 가능
4. DB뿐 아니라 인증키 같은 data도 공유 가능
5. 원하는 앱의 ContentProvider 접근은 Manifest 파일에 authorities 설정

```xml
<application>
    <provider android:name=".provider.DataProvider"
        android:authorities="eomy.github.com.contentproviderdata" />
</application>
```



----
**ref :**  
[android developer docs - Content provider basics](https://developer.android.com/guide/topics/providers/content-provider-basics)  
[예제 - 연락처 데이터](https://bitsoul.tistory.com/155)
