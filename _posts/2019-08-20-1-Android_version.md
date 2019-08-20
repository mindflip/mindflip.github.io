---
title:  "Android Versions"
excerpt: "버전별 특징 및 버전 점유율"

categories:
  - Android

last_modified_at: 2019-08-20T18:30:00
---

![version](/assets/images/posts/190820/version.png)

- 안드로이드는 구글과 [오픈 핸드셋 얼라이언스(OHA)](https://ko.wikipedia.org/wiki/%EC%98%A4%ED%94%88_%ED%95%B8%EB%93%9C%EC%85%8B_%EC%96%BC%EB%9D%BC%EC%9D%B4%EC%96%B8%EC%8A%A4)가 함께 개발한 모바일 중심의 운영체제
- 위의 안드로이드 공식페이지에서는 1.0, 1.1이 no codename 으로 나오지만, 비공식적으로 각각 ```애플 파이(apple pie) or 아스트로 보이(astro boy) / 프티 푸르(Petit Four) or 바나나 브레드(banana bread)``` 라고 불렸다고 한다.
- 버전이 하나씩 증가할 때마다 code name의 알파벳 또한 하나씩 증가

----

- ### 안드로이드를 개발해본 초짜 입장에서 가장 크게 다가온 건, Mashmellow의 권한 획득 부분
- 롤리팝 (API level 22) 이하의 버전들은 AndroidMenifest.xml에 권한을 등록하면 앱을 다운로드 받을 시 권한을 한 번만 획득
- 꺼림칙하면 앱 자체를 사용하지 않아야하는 방법밖에 없음
- 사용자 입장에서 문제가 많이 생길 수 있는 조건 (ex.한 앱이 44개의 권한 요청-피싱앱)
- 앱에서 해당 권한이 필요할때마다 사용자로부터 권한을 허가받도록 변경
- 사용자가 권한을 허가했더라도 사용자는 설정화면(설정 > 애플리케이션 > 앱이름 > 권한)을 통해 언제든지 권한을 허용/거부 가능

----

- 버전 별 점유율 (현재 2019. 08. 20)
- 오레오, 누가, 마시멜로 순으로 최고 점유율
![distribution](/assets/images/posts/190820/chart.png)

----

**ref :**  
[https://developer.android.com/about/dashboards](https://developer.android.com/about/dashboards)  
[https://source.android.com/setup/start/build-numbers](https://source.android.com/setup/start/build-numbers)  
[나무위키 안드로이드 버전](https://namu.wiki/w/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C(%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)/%EB%B2%84%EC%A0%84)
