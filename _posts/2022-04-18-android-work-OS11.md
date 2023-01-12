---
date: 2022-04-18
title: "[Android] 안드로이드 11 대응 - 패키지 공개 상태 변경 사항"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
## 🎯 targetVersion 30, 안드로이드 11 대응 🧑‍🎄

얼마만에 포스팅인지...!  
현업에서 기존 프로젝트의 min/target 버전을 변경하면서 안드로이드 11 대응을 준비하고 있다. 마이그레이션 하는 과정에서 기억해야 할 내용들을 포스팅하고자 한다.  
&nbsp;  
그중에서도 안드로이드 11 부터는 앱에서 단말에 설치된 다른 앱 목록을 가져올 수 없다. 대신 미리 매니페스트 파일에 지정한 앱의 정보만 가져올 수 있다. PackageManager 사용에 제약이 걸린 것이다.  
&nbsp;  

---

### ⛺ 패키지 공개 상태 변경 사항   
- targetSdkVersion 30 일 경우, 설치된 다른 앱 목록 가져올 수 없음    
- 알고 싶은 다른 앱 정보를 지정해야 함    
- `AndroidManifest.xml` 파일에 `<queries>` 요소로 특정 앱 패키지명 명시  
&nbsp;  

### ⛺ 영향받는 PackageManager API 목록  
- PackageManager.getPackageInfo  
- PackageManager.getInstalledPackage  
- PackageManager.queryIntentActivities  
&nbsp;  

### ⛺ AndroidManifest.xml 파일 수정  
- `<queries>` 추가 하여 특정 앱을 지정한다.  
  - 특정 앱의 패키지명 지정  
  - 특정 인텐트 필터 지정  

```
<manifest package="com.khs.example">
    <queries>
            <package android:name="com.khs.example1" /> // 패키지명
            <package android:name="com.khs.example2" />
            <intent>
                <action android:name="android.intent.action.SEND" />
                <data android:mimeType="image/*" />
            </intent>
    </queries>
```
{: .notice--primary}  

&nbsp;  

### ⛺ QUERY_ALL_PACKAGES  
- 안드로이드에서는 권장하지 않는 방법인데, 설치된 모든 앱을 확인할 수 있도록 허용하려면 `QUERY_ALL_PACKAGES` 권한을 부여하면 된다.  

```
<uses-permission android:name="android.permission.QUERY_ALL_PACKAGES" />
```
{: .notice--primary}  

&nbsp;  
&nbsp;  
[참고]  
<https://tech.buzzvil.com/blog/tech-blog-package-visibility-in-android-11/>  
