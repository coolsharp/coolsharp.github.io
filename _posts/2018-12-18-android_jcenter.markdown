---
layout: post
title:  "Android lib jcenter 업로드"
date:   2018-12-18 16:00:00 +0900
categories: android library
---

## 내가만든 라이브러리를 전세계 사람들과 공유하자
___
안드로이드에서 자주 사용하는 기능을 모듈로 만들고 많은 사람들이 함께 이용할 수 있게 github에 배포를 할 수 있다.

좀 더 나아가 소스코드 다운로드 없이 아래와 같이 gradle에서 한줄의 코드로 aar 파일을 다운로드 후 빌드까지 되게 할 수 있다.

```groovy
implementation 'com.coolsharp.animationclockview:0.1'
```

해당 모듈을 오픈하여 다른 개발자들이 쉽게 이용할 수 있게 jcenter에 업로드를 하는 방법이 있다.

이 강좌는 안드로이드 라이브러리를 생성하는 방법은 기술하지 않고 jcenter에 라이브러리 업로드 하는 방법에 대해 기술한다.

공유 저장소를 이용하는 방법에는 여러가지가 있지만 그 중 bintray를 통해 maven 저장소로 배포하는 방법이다.

<br>
<center><h1>. . .</h1></center>
<br>

## bintray 가입
___
https://bintray.com/로 이동하여 가입을 한다.(가입절차는 매우 쉬으므로 설명은 생략한다.)

![자세한 설명은 생략한다](/static/img/gallery/image_001.jpg)

<br>
<center><h1>. . .</h1></center>
<br>

## maven 저장소 생성
___
가입이 완료되었다면 로그인 후 레파지토리를 생성한다.

일반적으로 레파지토리 명은 maven으로 한다.<br>

![레파지토리 생성](/static/img/post/2018-12-18-android_jcenter/android_jcenter_01.png)

API 키를 확인한다.

![API 키 확인](/static/img/post/2018-12-18-android_jcenter/android_jcenter_02.png)

<br>
<center><h1>. . .</h1></center>
<br>

## Android Studio 라이브러리에 bintray 설정
___
안드로이드 스튜디오 라이브러리로 이동한다.

Project(build.gradle)에 다음과 같이 classpath를 추가한다.

<script src="https://gist.github.com/coolsharp/3f3434a24adb1f300a354acdffaad985.js"></script>

Module(build.gradle)에 다음과 같이 설정을 추가한다.

<script src="https://gist.github.com/coolsharp/1aad148423502187b992f5189a742f6a.js"></script>

terminal에서
```
./gradlew clean build bintrayUpload -PbintrayUser=[사용자 이름] -PbintrayKey=[API KEY] -PdryRun=false
```
와 같이 입력한다.

정상적으로 빌드가 되었다면 등록이 잘 된 것이다.

<br>
<center><h1>. . .</h1></center>
<br>

## 등록된 라이브러리를 사용하자
___
사용하는 방법은 아래와 같이 프로젝트 설정에 추가한다.

```groovy
 allprojects {	
     repositories {	
         ...	
         maven {	
             url  "https://dl.bintray.com/your-bintray-username/maven"	
         }	
     }	
 }	
```	

아래와 같이 implementation에 path를 추가한다.

```groovy
 implementation 'com.coolsharp.animationclock:animation-clockview:0.1'	
```