---
layout: post
title:  "안드로이드 웹 <-> 앱 연동"
date:   2019-10-31 12:00:00 +0900
tags: android webview
categories: android
---
## 안드로이드 웹 <-> 앱 연동
### 안드로이드 하이브리드 개발에 대해...

안드로이드 앱을 개발하는 방법 중에 네이티브 코드와 웹뷰 코드를 적절히 혼재하여 사용하는 하이브리드 개발 방식이 많이 쓰인다. 하이브리드 개발 방법 중 웹뷰는 앱 업데이트 없이 서버 배포로 내용을 변경 할 수 있는 장점이 있으나 네이티브에 비하여 실행 속도 및 UX 측면에서 다소 자연스러움이 떨어진다. 하지만 최근 앱 내 웹뷰의 랜더링 품질이 높아지고 디바이스가 고성능으로 출시가 되고 있어 이전에 비해 웹뷰로 개발된 영역의 품질이 네이티브에 비해 크게 차이가 나지 않고 있다.

<h3 align="center">. . .</h3>

### 안드로이드 웹 <-> 앱 연동의 필요성
웹뷰에서는 보안상의 사유로 디바이스 자원을 100% 사용할 수 없다. 서비스를 운영중 디바이스 자원이 필요할 경우가 있다. 예로, 특정 디바이스의 중복 체크를 위한 디바이스 유일값을 체크할 경우가 있다. 보통 안드로이드 경우 디바이스의 유일값을 Android id를 사용하는데 디바이스 영역으로 웹뷰에서 바로 접근하여 추출 할 수 없다. 하지만 네이티브에서는 해당 값을 자유롭게 추출 가능하다.이와 같은 경우에 웹뷰와 네이티브의 연동을 통해 값을 전달한다.

<h3 align="center">. . .</h3>

### 웹뷰와 네이티브 연동 개념
웹뷰와 네이티브 연동을 하기 앞서 앱 내 구성도를 설명한다.

#### 자바스크립트에서 네이티브 메소드 호출
![자바스크립트에서 네이티브 메소드 호출](/static/img/post/2019-10-31-android_webview/91c83a50.png)
1. 자바 스크립트에서 네이티브 코드를 호출한다.
2. 네이티브 코드가 JavaScriptinterface 어노테이션이 지정되었는지 확인하고 지정되어 있으면 네이티브 메소드를 실행한다.
3. 네이티브 메소드의 실행결과를 반환한다.

#### 네이티브에서 자바스크립트 호출
![네이티브에서 자바스크립트 호출](/static/img/post/2019-10-31-android_webview/c1c393c1.png)
1. evaluateJavascript를 통해 자바스크립트 호출한다.
2. 실행결과를 반환한다.

<h3 align="center">. . .</h3>

### 보안 주의 사항
본 연동방식은 안드로이드 OS 4.1 JELLY_BEAN 이하 디바이스에서는 보안상 문제가 있으므로 안드로이드 OS 4.2 이상에서 사용을 권장한다.
*안드로이드 OS 4.1 이하에서는 @JavaScriptinterface 어노테이션이 동작하지 않습니다.*


### 코드 작성
#### 네이티브 코드 작성
##### 웹뷰 셋팅
자바스크립트가 동작 할 수 있도록 기본 셋팅을 합니다.
```java
public void webviewInit() {
    WebSettings settings = webView.getSettings();
    // Javascript 사용하기
    settings.setJavaScriptEnabled(true);
    // WebView 내장 줌 사용여부
    settings.setBuiltInZoomControls(true);
    // 화면에 맞게 WebView 사이즈를 정의
    settings.setLoadWithOverviewMode(true);
    // ViewPort meta tag를 활성화 여부
    settings.setUseWideViewPort(true);
    // 줌 컨트롤 사용 여부
    settings.setDisplayZoomControls(false);
    // 사용자 제스처를 통한 줌 기능 활성화 여부
    settings.setSupportZoom(false);
    // TextEncoding 이름 정의
    settings.setDefaultTextEncodingName("UTF-8");

    // Setting Local Storage
    settings.setDatabaseEnabled(true);
    settings.setDomStorageEnabled(true);

    // 캐쉬 사용 방법을 정의
    settings.setCacheMode(WebSettings.LOAD_NO_CACHE);
}
```
##### 앱 내 콜백 인터페이스 작성
자바스크립트에서 호출할 메소드의 형태를 정의합니다.
```java
public interface CustomJavaScriptCallback {

    String webViewToApp(int valueA, int valueB);

    String appToWebViewNative();
}
```
##### 앱 내 콜백 메소드 구현 및 추가
자바스크립트에서 호출할 메소드를 구현합니다.
```java
// 웹뷰 자바 스크립트 인터페이스 추가(인터페이스 명 : WebViewCallbackInterface)
webView.addJavascriptInterface(new CustomJavaScriptCallback() {
    /**
     * 웹에서 네이티브 메소드 호출
     * @param valueA 인자
     * @param valueB 인자
     * @return 반한값
     */
    @JavascriptInterface
    @Override
    public String webViewToApp(int valueA, int valueB) {
        return "계산 결과 : " + (valueA + valueB);
    }

    /**
     * 웹뷰에서 호출할 수 없는 메소드
     * @return 반환값
     */
    @Override
    public String appToWebViewNative() {
        return "접근불가";
    }
}, "WebViewCallbackInterface");
```
##### 앱 내 콜백 메소드 구현 및 추가
네이티브에서 evaluateJavascript로 자바스크립트를 호출합니다.
```java
findViewById(R.id.button).setOnClickListener(
                view -> webView.evaluateJavascript("javascript:executeFunction(\"앱에서 웹뷰 스크립트 호출\");"
                , value -> Toast.makeText(MainActivity.this, value.replace("\"", ""), Toast.LENGTH_SHORT).show()));
```
##### HTML 작성
HTML 코드를 작성합니다.
```javascript
<html>
<head>
    <meta name="viewport" content="width=device-width, user-scalable=no">
    <script language="JavaScript">
        // 웹뷰에서 네이티브 메소드를 호출하여 값을 받아옴
    function webViewToApp() {
      alert(WebViewCallbackInterface.webViewToApp(1, 2));
    }

        // 웹뷰에서 접근 허용되지 않은 네이티브 메소드를 호출
    function appToWebViewNative() {
      alert(WebViewCallbackInterface.appToWebViewNative());
    }

        // 네이티브에서 자바 스크립트를 호출
    function executeFunction(value) {
      alert(value);
      return '네이티브로 반환';
    }
    </script>
</head>

<body>
<div id="text"></div>
<hr/>
<h2>JavaScript <-> Android WebView Callback Interface Sample</h2>
<hr/>
<input type="button" style="HEIGHT: 60pt" value="1 + 2 앱 호출하여 계산하기" onclick="webViewToApp()"/>
<br>
<br>
<input type="button" style="HEIGHT: 60pt" value="접근불가 메소드 호출" onclick="appToWebViewNative()"/>
</body>

</html>
```

<h3 align="center">. . .</h3>

#### 동작 확인
##### 자바스크립트에서 네이티브 메소드 실행
![자바스크립트에서 네이티브 메소드 실행](/static/img/post/2019-10-31-android_webview/01.gif)

<h3 align="center">. . .</h3>

##### 자바스크립트에서 @JavaScriptinterface 추가하지 않은 네이티브 메소드 실행
![자바스크립트에서 @JavaScriptinterface 추가하지 않은 네이티브 메소드 실행](/static/img/post/2019-10-31-android_webview/02.gif)
접근할 수 없는 메소드 호출 시 아래와 같은 오류 발생
[INFO:CONSOLE(12)] "Uncaught TypeError: WebViewCallbackInterface.appToWebViewNative is not a function", source: file:///android_asset/sample.html (12)

<h3 align="center">. . .</h3>

##### 네이티브에서 자바스크립트 호출
![네이티브에서 자바스크립트 호출](/static/img/post/2019-10-31-android_webview/03.gif)