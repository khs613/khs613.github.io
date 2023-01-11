---
date: 2022-12-26
title: "[Android] 안드로이드 Flavor 구성하기"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
#### Android Flavor 사용하기

한개의 앱에서 여러 버전의 앱을 만들고자 할 때, 안드로이드 Flavor를 사용하면 앱을 구분할 수 있다. 같은 기능에 무료/유료 버전, SDK 버전 등에 따라 앱을 구분하고 싶을 때 사용하는 Flavor를 알아보자.  
&nbsp;  

---

##### build.gradle 구성  
예시로 무료 버전과 유료 버전으로 구분할 때 Flavor 구성을 해보겠다.  
build.gradle(app) 파일에서 `productFlavors` 블록에 원하는 버전을 블록으로 만들어서 각각 설정을 해준다. 무료 버전인 free와 유료 버전인 paid로 추가했다.  

```
android {
    flavorDimensions "version"

    productFlavors {
        free {
            dimension "version"
            applicationIdSuffix ".free"
            buildConfigField 'boolean', 'ISFREE', "true"
        }
        paid {
            dimension "version"
            applicationIdSuffix ".paid"
            buildConfigField 'boolean', 'ISFREE', "false"
        }
    }
    ...
```
{: .notice--primary}  

- **flavorDimensions** : 더 많은 버전의 조합을 사용하고자 할 때 해당 속성을 사용한다.  
buildType, productFlavors 과 더 많은 조합의 버전을 생성할 수 있다.  
- **applicationIdSuffix** : applicationId 뒤에 붙게 된다.  
패키지명이 'com.example.flavor' 라면 여기서 +'.free' 가 붙으면서 최종적으로 'com.example.flavor.free' 가 된다.  
- **buildConfigField** : BuildConfig.#### 로 사용  
BuildConfig.ISFREE의 값을 true/false 로 설정한다는 내용이다.  

![Flavor](/assets/img/post/2022-12-26-1/img_1.png)  

build.gralde 구성이 끝나고 Sync Now 를 해주면 사진과 같이 **Build Variants**에 4개가 생긴것을 확인 할 수 있다. free/paid 버전으로 각각 Debug, Release가 생겼고 빌드 시 선택해서 빌드하면 된다.  
