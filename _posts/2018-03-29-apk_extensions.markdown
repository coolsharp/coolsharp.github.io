---
layout: post
title:  "Google Play APK Extensions"
date:   2018-03-29 06:00:00 +0900
tags: android apk_excensions
categories: android
---

## 100Mb 용량을 초과하는 앱을 개발하였다면...
___
앱의 특성에 따라 미디어 라이브러리가 많이 추가되어 100Mb를 넘기는 경우가 발생할 수 있다.

Google Play 콘솔에서 APK를 등록할 때 최대 제한 용량은 100Mb 이다.

하여 100Mb를 초과하는 APK를 구글 플레이에 등록이 불가하다.

하지만 [`google play apk extensions library`](https://support.google.com/googleplay/android-developer/answer/2481797?hl=ko)를 이용하면 단일 앱은로는 아니지만 확장 파일을 이용하여 최대 4.1GB까지 등록할 수 있다.

`Google Play APK Extensions library`를 이용하게 될 시 1개의 앱에 최대 담을 수 있는 용량은 아래와 같다.
- APK : 100MB
- Main Extension : 2GB
- Patch Extension : 2GB

이제 `Google Play APK Extensions library`를 이용하여 확장 다운로드를 활용하는 방법에 대해 알아보자.
<br>
<center><h1>. . .</h1></center>
<br>

## Google Play APK Extensions 적용
___
적용 방법은 [`google play apk extensions library 가이드`](https://developer.android.com/google/play/expansion-files.html) 문서에 자세히 기록되어 있다.

하지만 대부분의 레퍼런스 문서는 딱딱한 문체로 인하여 이해하기까지에는 많은 시간이 필요하다.

아울러 문서에는 기입되어 있지 않고 맨땅에 헤딩하면서 습득한 경험도 공유하기 위해 별도의 글로 내용을 정리한다.
<br>
<center><h1>. . .</h1></center>
<br>

### 1. 환경구성
___
Android Studio에 `Google Play APK Extensions library`를 설치하자.

![레파지토리 생성](/static/img/post/2018-03-29-apk_extensions/image01.png)

<br>
<center><h1>. . .</h1></center>
<br>

### 2. 코드작성
___

<br>
<center><h1>. . .</h1></center>
<br>

### 3. 테스트
___

<br>
<center><h1>. . .</h1></center>
<br>

### 4. 배포
___

<br>
<center><h1>. . .</h1></center>
<br>

### 5. 다운로드
___
