---
date: 2021-02-14
title: "[Macbook] 맥 OS에서 ADB 사용하는 방법"
categories: Macbook
tags:
    - macbook
    - adb
toc: true
toc_sticky: true
---
#### 맥북에서 ADB 사용하는 방법  
맥에서 안드로이드 개발을 하면서 ADB를 사용하려고 하는데, 어떻게 사용해야 할지 알아보자.  
&nbsp;  

##### ADB(Android Debug Bridge)  
Android 디버그 브리지([adb](https://developer.android.com/studio/command-line/adb?hl=ko))는 기기와 통신할 수 있는 다목적 명령줄 도구이다. adb 명령어는 앱의 설치 및 디버깅과 같은 다양한 기기 작업에 도움이 되며, 기기에서 다양한 명령어를 실행하는 데 사용할 수 있는 Unix 셸에 관한 액세스를 제공한다.  

##### Android SDK 설치  
adb는 Android SDK 플랫폼 도구 패키지에 포함되어 있다. 이 패키지는 SDK Manager를 사용하여 다운로드할 수 있고, 독립형 Android SDK 플랫폼 도구 패키지를 따로 다운받을 수 있다.  
- [SDK 다운로드 링크](https://developer.android.com/studio/releases/platform-tools?hl=ko)  
![adb](/assets/img/post/2021-02-14-1/img_1.png)  
- android_sdk/platform-tools/에 설치된다.  

##### ADB 환경변수 설정  
매번 SDK가 설치되어 있는 경로로 찾아가서 ADB를 사용하는 것은 매우 귀찮은 일이기 때문에, 디렉토리를 입력하지 않고도 ADB 사용할 수 있는 환경변수 설정을 해보자.  
- `.bash_profile` 파일 위치 확인  

$ls .bash_profile
{: .notice--primary}  

- 단축키 제공되는 `nano`이용해 파일 편집  

nano .bash_profile
{: .notice--primary}  

- 환경변수 설정 코드 입력  
  - 아래 코드 위치와 동일하지 않다면, 본인 컴퓨터의 sdk 설치 위치를 적어주면 된다.
  - 입력 후 `ctrl + X` 누르고 `Y(yes)` 입력하면 저장된다.    

export PATH=$PATH:/Users/사용자이름/Library/Android/sdk/platform-tools/
{: .notice--primary}  
![adb](/assets/img/post/2021-02-14-1/img_2.png)  

- 제대로 설정 됐는지 확인  
  - 수정된 .bash_profile을 source 입력으로 다시 적용시켜 주고,  
  - adb version 입력 후 정확하게 버전이 나오면 완료  

source ~/.bash_profile
adb version
{: .notice--primary}  
![adb](/assets/img/post/2021-02-14-1/img_3.png)  

&nbsp;  
이제 어디서든 ADB 사용 가능해졌다!

&nbsp;  
&nbsp;  
[참고]  
<https://developer88.tistory.com/174>  
