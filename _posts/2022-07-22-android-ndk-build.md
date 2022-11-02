---
date: 2022-07-22
title: "[Android] 맥북 M1 에서 NDK 빌드 오류 해결"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
#### 맥북 M1 에서 NDK 빌드 오류 해결

안드로이드 ndk 빌드 중 만난 오류 녀석들...  
기존 프로젝트 소스 중 native code 를 수정해야 할 일이 생겼다. 따로 히스토리가 없어 한참을 찾다가 ndk 빌드가 필요한 상황이었는데,
별도의 ndk 버전 정보가 없어서 맞는 버전 찾는 것도 일이었다. 어쨌든 지금은 해결한 상황인데, 며칠동안 붙잡고 해결한게 아까워서 남겨본다!😎  

##### Android NDK 빌드 툴  
<b>CMake</b>  
- CMakeLists.txt 파일 필요  
- Android, Linux, Windows, iOS 등 모든 타겟에서 빌드 가능  

<b>NDK-Build</b>  
- Andorid.mk, Applicaton.mk 파일 필요  

기존 프로젝트 jni 폴더에 Android.mk 파일이 있었기 때문에 NDK-Build 를 통해 빌드를 진행했다.  

##### No toolchains found in the NDK toolchains folder for ABI with prefix: arm-linux-androideabi  
- 안드로이드에서 사용되는 NDK 버전이 올라가면서 MIPS형 CPU에 대한 지원이 중단되었다는 에러라고 한다.  
- gradle 버전이 낮으면 안드로이드 스튜디오가 MIPS에 대한 정보를 찾으려다가 위와 같은 에러 발생  

<b>해결방법</b>  
- gradle 버전 올린 후 안드로이드 스튜디오 재실행  
- build.gradle 파일에서 gradle 버전 3.1.4 이상으로 설정  
- 하지만 이미 해당 프로젝트는 gradle 버전이 3.5.2 인 상태  
- ndk 버전 중 맞는 버전 apply 시켜주기 (ndk 21.4.7075529 버전으로 맞춤)  
- 나의 경우 ndk 버전을 다운 그레이드 시켜주니 해당 에러는 없어졌다! 하지만 다음과 같은 에러가 발생한다🤯  

##### ERROR: Unknown host CPU architecture: arm64  
- 구글링 해보니 맥북 프로 M1에서 발생하는 이슈라고 한다.  
- 그렇다면 windows OS 에서는 정상 동작할 수 있다는 건데, 내 컴퓨터가 맥북 M1이기 때문에 해결 할 수 밖에 없다.  

<b>해결방법</b>  
- ndk 폴더로 이동하여 `ndk-build` 편집  
 - 맥북 ndk 경로 : /.../Library/Android/sdk/ndk 참고!  
- AS-IS  
```
#!/bin/sh
DIR="$(cd "$(dirname "$0")" && pwd)"
$DIR/build/ndk-build "$@"
```
{: .notice--primary}  
- TO-BE
```
#!/bin/sh
DIR="$(cd "$(dirname "$0")" && pwd)"
arch -x86_64 /bin/bash $DIR/build/ndk-build "$@"
```
{: .notice--primary}  
&nbsp;  
이렇게 하고서 ndk 빌드 했더니 드디어 성공!  
빌드하려는 프로젝트의 경우 32비트용, 64비트용 모두 빌드가 필요해서 발생한 이슈가 아닐까 싶다.  

&nbsp;  
&nbsp;  
[참고]  
<https://machine-woong.tistory.com/398>  
<https://exchangetuts.com/unknown-host-cpu-architecture-arm64-android-ndk-siliconm1-apple-macbook-pro-1640617266175701>  
<https://overface.tistory.com/m/428>  
