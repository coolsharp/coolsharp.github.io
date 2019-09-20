---
layout: post
title:  "Flutter assets 관리"
date:   2019-09-20 12:00:00 +0900
tags: flutter assets
categories: flutter
---

## Flutter에서 Asserts 관리
---
### Flutter에서 Asserts를 관리하는 방법을 기술한다.

#### 1. Asserts 폴더 생성
- Asserts 폴더는 아래위치에 생성
```text
프로젝트 폴더 \ assets
```
<h3 align="center">. . .</h3>

#### 2. Asserts 폴더 생성
- Asserts 폴더 하위에 원하는 파일 추가

<h3 align="center">. . .</h3>

#### 3. pubspec.yaml에 assets 설정
- pubspec.yaml에 아래와 같이 폴더 지정
```java
flutter:

  assets:
    - assets/img/

```

- 또는 파일별 지정 가능
```java
  assets:
    - assets/img/coolsharp.png

```

<h3 align="center">. . .</h3>

#### 4. assets 파일 코드에서 불러오기
- 코드에 아래와 같이 assets 파일 사용
```java
return Container(
    constraints: BoxConstraints.expand(height: 300),
    alignment: Alignment.center,
    child: Image.asset(
      "assets/img/coolsharp.png",
      fit: BoxFit.cover,
    ));
```
