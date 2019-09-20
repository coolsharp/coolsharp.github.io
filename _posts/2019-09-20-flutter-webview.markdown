---
layout: post
title:  "Flutter WebView"
date:   2019-09-20 16:00:00 +0900
tags: flutter webview
categories: flutter
---

## Flutter WebView 적용
---
### Flutter에서 WebView를 적용하는 방법을 기술한다.

#### 1. pubspec.yaml에 dependencies 추가
- pubspec.yaml에 아래와 같이 dependencies를 추가

  ```java
  dependencies:
    flutter:
      sdk: flutter

    ...
    webview_flutter: ^0.3.10+4
  ```

<h3 align="center">. . .</h3>

#### 2. Info.plist에 key 추가
- Info.plist에 아래와 같이 key 추가

  ```xml
  <key>io.flutter.embedded_views_preview</key>
  <true/>
  ```

<h3 align="center">. . .</h3>

#### 3. 코드에 WebView 추가

  ```java
  import 'package:webview_flutter/webview_flutter.dart';
  ...
  body: new WebView(
    initialUrl: 'https://coolsharp.github.io/', // 초기 로딩 url
    javascriptMode: JavascriptMode.unrestricted, // 자바 스크립크 켜기
    onPageFinished: (String url) { // 페이지 완료시 이벤트
      print('finished:' + url);
    },
  ),
  ...
  ```