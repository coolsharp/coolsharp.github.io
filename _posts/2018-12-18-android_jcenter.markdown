---
layout: post
title:  "Android lib jcenter 업로드"
date:   2018-12-18 16:00:00 +0900
categories: jekyll update
---

## Android lib jcenter 업로드
안드로이드에서 자주 사용하는 기능을 모듈로 만들고 많은 사람들이 함께 이용할 수 있게 github에 배포를 할 수 있다.
좀 더 나아가 소스코드 다운로드 없이 aar 파일을 gradle에서 한줄의 코드로 다운로드 및 빌드까지 되게 할 수 있다.

    implementation 'com.coolsharp.animationclockview:0.1'

해당 기능일 여러사람이 쉽게 이용하게 하기위헤서는 jcenter에 업로드를 하는 방법이 있다.
