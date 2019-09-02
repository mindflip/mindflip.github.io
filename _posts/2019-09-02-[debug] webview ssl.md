---
title:  "[Debug] Andorid Webview 흰 화면 (SSL 문제)"
excerpt: "SSL 적용된 웹페이지 로딩 안 되는 문제"

categories:
  - Android
  - webview

last_modified_at: 2019-09-02T19:30:00
---

> WebView에서 유효하지 않은 인증서 에러 발생 시 무시 처리 방법(SSL 에러)

웹으로 만들어진 모바일용 화면을 안드로이드 앱을 통해서 디스플레이해줘야하는 일이 생겼다.

그래서 Webview 객체를 이용해 기본 세팅을 해주고 세팅된 URL을 Load시켰다.

회사에서 원하는 것은 모바일이 아닌 셋톱박스에 올라간 안드로이드 OS 에서 앱을 실행하는 것이었다.

모바일에서는 잘 보였는데, 셋톱박스에서는 이상하게 흰 화면으로 고정되어 있었다.

찾아보니 SSL 문제란다.

----
### 해결방법

- WebViewClient 객체의 `onReceivedSslError` 콜백메서드에서 에러가 나도 진행한다는 것을 명시

```java
mWebView = new WebView(getActivity());
mWebView.setWebViewClient(new WebViewClient() {

    @Override
    public void onReceivedSslError(WebView view,
            SslErrorHandler handler, SslError error) {
        handler.proceed();
    }
});
```

이번 개발은 디버깅으로 빌드하여 apk를 넘겨주어도 되는 경우여서 별 일이 없었지만, 마켓에 올려야하는 경우 보안 경고를 받는단다.
따라서, dialog를 띄워 해결하는 방법도 생각해볼 수 있다.

----

ps.  
추가로 Ajax를 불러와야하는 페이지에선
> The request /response that are contrary to the Web firewall security policies have been blocked

에러가 뜨면서 Load가 되지 않았다.
도저히 방법을 못 찾겠어서 그냥 웹 소스에서 Ajax를 제거하는 방법으로 해결했다... 고민해봐야할 문제다.  
나중에 WebView 세팅과 응용하는 포스팅을 다뤄봐야겠다.

----
**ref :**  
[android webview 로드시 ssl(https) 보안인증서 문제](https://jinmanp.tistory.com/entry/android-webview-%EB%A1%9C%EB%93%9C%EC%8B%9C-sslhttps-%EB%B3%B4%EC%95%88%EC%9D%B8%EC%A6%9D%EC%84%9C-%EB%AC%B8%EC%A0%9C)  
[웹뷰(webview) 하얗게 나오는 경우(ssl인증 무시하기)](https://minaminaworld.tistory.com/85)  
[WebView SSL 오류 핸들러 해결 방법](http://blog.naver.com/PostView.nhn?blogId=ms76k&logNo=220914291602)
