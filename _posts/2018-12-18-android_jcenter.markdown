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

이 강좌는 안드로이드 라이브러리를 생성하는 방법은 기술하지 않는다.

![자세한 설명은 생략한다](https://s3.namuwikiusercontent.com/s/2b38937bb1ead788420b12c0f2f31d441cfc8af59d3fba718c03085bd37cacece7eaae2bc0e47717d99177eb018bd48b66075acf90a58840228eeb6fa02eeca14a417ad7b69e8fb704c7bfe48ab5c4ae025bb61179548d65c52b8ae964ee6358)

jcenter에 라이브러리를 빌드하여 업로드 하는 방법만 기술한다.

여러가지 방법이 있지만 가장 간단한 방법은 bintray를 통해 maven 저장소로 배포하는 방법이다.

<br>
<center><h1>. . .</h1></center>
<br>

## bintray 가입
___
https://bintray.com/로 이동하여 가입을 한다.(가입 등의 설명은 생략한다.)


## maven 저장소 생성
___
레퍼지토리를 생성해야 한다.

일반적으로 maven으로 생성한다.<br>

![레파지토리 생성](/static/img//android_jcenter_01.png)

API 키를 확인한다.

![API 키 확인](/static/img/android_jcenter_02.png)


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