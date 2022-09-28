---
date: 2022-05-05
title: "[Android] 안드로이드 11 대응 - File Provider"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
#### FileProvider, 안드로이드 11 대응

안드로이드 11에서는 파일 읽기/쓰기 및 접근 하는 방식에 많은 제약이 생겼는데,  
그 중 앱에서 다른 앱으로 파일을 공유할 때 정책이 변경되었다.  
&nbsp;  
데이터 공유 시에는 intent 로 전송하는데, 파일을 공유할 때는 콘텐츠의 URI를 전송하고 수신할 앱에 대해서만 임시 액세스 권한을 부여하고 자동 만료되도록 동작된다.  

##### AndroidManifest.xml 에서 FileProvider 지정   
- `<provider>` 추가 하여 콘텐츠 URI 생성에 사용할 권한을 지정한다.  
- 공유 디렉터리를 지정하는 XML 파일을 resource 로 지정  
- `grantUriPermissions` true 로 설정해줘야 temp 권한을 획득할 수 있다.  

```
<provider
  android:name="androidx.core.content.FileProvider"
  android:authorities="com.khs.example.provider"
  android:exported="false"
  android:grantUriPermissions="true">
  <meta-data
    android:name="android.support.FILE_PROVIDER_PATHS"
    android:resource="@xml/provider_paths"/>
</provider>
```
{: .notice--primary}  

##### 공유 디렉터리 지정   
- res/xml/provider_paths.xml 추가  
- 미리 file-path 를 지정하여 URI를 생성  
- paths 태그 안에 여러개의 file-path 를 기재할 수 있다.  

```
<?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
  <files-path name="files" path="."/>
  <external-files-path name="external_files_path" path="." />
  <external-path name="storage/emulated" path="."/>
</paths>
```
{: .notice--primary}  

디렉터리 별 path  
- file-path : Context.getFilesDir()  
- cache-path : Context.getCacheDir()  
- external-path : Environment.getExternalStorageDirectory()  
- external-files-path : Context.getExternalFilesDir(String)  
- external-cache-path : Context.getExternalCacheDir()  
- external-media-path : Context.getExternalMediaDirs(), API 21 이상부터 가능  

&nbsp;  
&nbsp;  
[참고]  
<https://omod.tistory.com/97>  
<https://kikimihye.tistory.com/151>  
<https://aroundck.tistory.com/7287>  
