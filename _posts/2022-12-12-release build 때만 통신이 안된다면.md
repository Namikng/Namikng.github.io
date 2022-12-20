---
layout: post
title:  "release build 때만 통신이 안된다면"
date:   2022-12-12
last_modified_at: 
categories: [개발]
tags: [Flutter]
---

debug build(안드로이드 스튜디오에서 run으로 실행하던)에서는 잘만 되던 통신이 release build에선 갑자기 안된다면?

권한만 한줄 추가해주면 된다! 간단!

`project 경로/android/app/src/main/AndroidManifest.xml`

파일을 열어준다. **main 폴더 안으로** 들어가야함에 유의❗️

`<uses-permission android:name="android.permission.INTERNET" />` 

위 코드를 아래의 위치에 끼워넣어준다.
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="io.company.appName">
    <uses-permission android:name="android.permission.INTERNET" /> 
   <application
        android:label="appName"
```
이제 다시 실행해보면??

release build도, apk로 추출해서 실행해도 잘된다😄