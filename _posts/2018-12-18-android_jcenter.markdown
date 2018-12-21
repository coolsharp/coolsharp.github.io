---
layout: post
title:  "Android lib jcenter 업로드"
date:   2018-12-18 16:00:00 +0900
categories: jekyll update
---

## 내가만든 라이브러리를 전세계 사람들과 공유하자
안드로이드에서 자주 사용하는 기능을 모듈로 만들고 많은 사람들이 함께 이용할 수 있게 github에 배포를 할 수 있다.
좀 더 나아가 소스코드 다운로드 없이 aar 파일을 gradle에서 한줄의 코드로 다운로드 및 빌드까지 되게 할 수 있다.

    implementation 'com.coolsharp.animationclockview:0.1'

해당 기능일 여러사람이 쉽게 이용하게 하기위헤서는 jcenter에 업로드를 하는 방법이 있다.

안드로이드 라이브러리를 생성했다는 전제로 이어 시작한다.

여러가지 방법이 있지만 가장 간단한 방법은 bintray를 통해 maven 저장소로 배포하는 방법이다.
## bintray 가입
https://bintray.com/로 이동하여 가입을 한다.(가입 등의 설명은 생략한다.)

## maven 저장소 생성
레퍼지토리를 생성해야 한다.

일반적으로 maven으로 생성한다.<br>

![레파지토리 생성](https://github.com/coolsharp/coolsharp.github.io/raw/master/static/img//android_jcenter_01.png)

API 키를 확인한다.

![API 키 확인](https://github.com/coolsharp/coolsharp.github.io/raw/master/static/img/android_jcenter_02.png)

## Android Studio 라이브러리에 bintray 설정
안드로이드 스튜디오 라이브러리로 이동한다.

Project(build.gradle)에 다음과 같이 classpath를 추가한다.

```
    dependencies {
        classpath 'com.android.tools.build:gradle:3.2.1'
        classpath 'com.novoda:bintray-release:0.9'
    }
```
Module(build.gradle)에 다음과 같이 설정을 추가한다.
```
apply plugin: 'com.novoda.bintray-release'  
  
publish {  
  userOrg = 'coolsharp' // 사용자 이름
  groupId = 'com.coolsharp.animationclock' // 모듈 패키지 명
  artifactId = 'animation-clockview' // 모듈 id
  publishVersion = '0.1' // 버전
  desc = 'https://github.com/coolsharp/AnimationClock'  
  website = 'https://github.com/coolsharp/AnimationClock'  
  issueTracker = "https://github.com/coolsharp/AnimationClockissues"  
  repository = "https://github.com/coolsharp/AnimationClock.git"  
}
```

terminal에서 ./gradlew clean build bintrayUpload -PbintrayUser=[사용자 이름] -PbintrayKey=[API KEY] -PdryRun=false와 같이 입력한다.

정상적으로 빌드가 되었다면 등록이 잘 된 것이다.

```	
 allprojects {	
     repositories {	
         ...	
         maven {	
             url  "https://dl.bintray.com/your-bintray-username/maven"	
         }	
     }	
 }	
```	
 
```	
 implementation 'com.coolsharp.animationclock:animation-clockview:0.1'	
```