---
date: 2021-02-04
title: "[Android] INSTALL_FAILED_TEST_ONLY 에러 해결"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
## 🍡 INSTALL_FAILED_TEST_ONLY 에러 해결하기 🍪

APK를 adb로 설치 하려고 보니, 아래와 같은 에러가 발생하면서 앱을 설치 할 수 없었다.  
&nbsp;  
![android](/assets/img/post/2021-02-04-1/img_1.png)  

adb install -r *.apk
{: .notice--primary}

&nbsp;  

---

### 🍽 -t 옵션  
원래라면 `-r` 옵션으로 설치 가능했는데 무슨일인가 싶어서 찾아보니, TestOnly 앱으로 만들어지면 디버깅 가능한 앱이지만, 릴리즈 앱으로는 쓸 수 없다.  
Android Studio는 apk를 만들 때 AndroidManifest.xml에서 `testOnly` 속성을 설정할 수 있다. `testOnly=true` 일 때는 아래와 같이 `-t` 옵션을 주고 설치해야 한다.  

adb install -t *.apk
{: .notice--primary}

그러면 이렇게 설치 완료  
&nbsp;  
![android](/assets/img/post/2021-02-04-1/img_2.png)  

&nbsp;  

### 🍽 testOnly 속성  
만약 testOnly에 대한 설정을 하지 않았는데, 자동으로 TestOnly apk로 생성될 수 있다. 안드로이드 스튜디오에서 자동으로 `testOnly=true`로 설정하기 때문에 false로 설정하고 싶다면 `gradle.properties` 파일에서 false로 설정해주면 된다.  

android.ingected.testOnly=false
{: .notice--primary}

이렇게 설정하고 빌드하면 일반적인 apk가 생성되고, `-t` 옵션 없이 설치할 수 있다.  

&nbsp;  
&nbsp;  
[참고]  
<https://codechacha.com/ko/how-to-disable-testonly-in-android/>
