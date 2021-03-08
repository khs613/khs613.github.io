---
date: 2021-03-08
title: "[Android] DownloadManager로 파일 다운로드 받기"
categories: Android
tags:
    - android
    - downloadManager
toc: true
toc_sticky: true
---
#### DownloadManager 사용하기  
DownloadManager는 HTTP 다운로드를 처리하는 시스템 서비스이다.  
앱은 URI를 저장될 위치와 특정 파일로 다운로드 하도록 요청할 수 있다. 또한, 앱에서 별도의 스레드를 생성할 필요 없이, 내부의 백그라운드 서비스에서 다운로드를 수행한다.  
&nbsp;  
DownloadManager는 notification을 통해 사용자에게 다운로드 상태를 보여주며, 실시간으로 다운로드 상태를 체크할 수 있다. 다운로드가 완료되면 브로드캐스트를 통해 완료되었음을 알려준다.  
다음은 DownloadManager를 사용해서 파일을 다운로드 하는 과정이다.  

##### 인터넷 권한 설정  
- 매니페스트 파일에 인터넷 권한과 저장소 권한 추가  

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```
{: .notice--primary}  

##### 기본 설정  
- 다운받은 파일이 저장될 위치 설정  

``` java
private String outputFilePath = Environment.getExternalStoragePublicDirectory(
            Environment.DIRECTORY_DOWNLOADS + "/저장할 폴더 이름") + "/저장할 파일 이름.txt";
```
{: .notice--primary}  

- 브로드캐스트 리시버 등록  
  - ACTION_DOWNLOAD_COMPLETE : 다운로드가 완료되었을 때 전달  

``` java
@Override
public void onResume(){
    super.onResume();
    IntentFilter completeFilter = new IntentFilter(DownloadManager.ACTION_DOWNLOAD_COMPLETE);
    registerReceiver(downloadCompleteReceiver, completeFilter);
}

@Override
public void onPause(){
    super.onPause();
    unregisterReceiver(downloadCompleteReceiver);
}
```
{: .notice--primary}  

##### 다운로드 요청  
`DownloadManager.Request`을 설정하여 DownloadManager Queue에 등록하게 되면 큐에 들어간 순서대로 다운로드가 처리된다.  
`DownloadManager` 객체 생성하여 다운로드 대기열에 URI 객체를 넣는다.  

``` java
private DownloadManager mDownloadManager;
private Long mDownloadQueueId;
...
private void URLDownloading(Uri url) {
        if (mDownloadManager == null) {
            mDownloadManager = (DownloadManager) mContext.getSystemService(Context.DOWNLOAD_SERVICE);
        }
        File outputFile = new File(outputFilePath);
        if (!outputFile.getParentFile().exists()) {
            outputFile.getParentFile().mkdirs();
        }

        Uri downloadUri = url;
        DownloadManager.Request request = new DownloadManager.Request(downloadUri);
        List<String> pathSegmentList = downloadUri.getPathSegments();
        request.setTitle("다운로드 항목");
        request.setDestinationUri(Uri.fromFile(outputFile));
        request.setAllowedOverMetered(true);

        mDownloadQueueId = mDownloadManager.enqueue(request);
    }
```
{: .notice--primary}  

`Request` 설정 항목  
- DownloadManager.Request : Request 객체를 생성하며 인자로 다운로드할 파일의 URI를 전달한다.  

- setTitle : notification 제목  

- setDescription : notification 설명  

- setNotificationVisibility : VISIBILITY_VISIBLE로 설정되면 notification에 보여진다.  

- setDestinationUri : 파일이 저장될 위치의 URI  

- setRequiresCharging : true일 경우, 단말이 충전중일 때만 다운로드  

- setAllowedOverMetered : true일 경우, 모바일네트워크가 연결되었을 때도 다운로드  

- setAllowedOverRoaming : true일 경우, 로밍네트워크가 연결되었을 때도 다운로드  


##### 다운로드 상태 조회  
`DownloadManager.Query` 객체를 생성하고 `DownloadManager.query()`로 쿼리를 한다. cursor가 리턴되며 특정 칼럼을 조회하여 다운로드 상태를 가져온다.  

``` java
private BroadcastReceiver downloadCompleteReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {

        long reference = intent.getLongExtra(DownloadManager.EXTRA_DOWNLOAD_ID, -1);

        if(mDownloadQueueId == reference){
            DownloadManager.Query query = new DownloadManager.Query();  // 다운로드 항목 조회에 필요한 정보 포함
            query.setFilterById(reference);
            Cursor cursor = mDownloadManager.query(query);

            cursor.moveToFirst();

            int columnIndex = cursor.getColumnIndex(DownloadManager.COLUMN_STATUS);
            int columnReason = cursor.getColumnIndex(DownloadManager.COLUMN_REASON);

            int status = cursor.getInt(columnIndex);
            int reason = cursor.getInt(columnReason);

            cursor.close();

            switch (status) {
                case DownloadManager.STATUS_SUCCESSFUL :
                    Toast.makeText(mContext, "다운로드를 완료하였습니다.", Toast.LENGTH_SHORT).show();
                    break;

                case DownloadManager.STATUS_PAUSED :
                    Toast.makeText(mContext, "다운로드가 중단되었습니다.", Toast.LENGTH_SHORT).show();
                    break;

                case DownloadManager.STATUS_FAILED :
                    Toast.makeText(mContext, "다운로드가 취소되었습니다.", Toast.LENGTH_SHORT).show();
                    break;
            }
        }
    }
};
```
{: .notice--primary}  

- 브로드캐스트에서 다운로드 상태를 조회하는 코드이다. 다운로드 상태는 아래와 같은 값을 반환한다.  
   - STATUS_SUCCESSFUL  
   - STATUS_FAILED  
   - STATUS_RUNNING  
   - STATUS_PAUSED  

<img src = "/assets/img/post/2021-03-08-1/img_1.jpg" width="50%">  
&nbsp;  
이렇게 다운로드 할 때 사용자가 notification을 통해 다운로드 상황을 볼 수 있다. notification은 DownloadManager에서 구현된 부분이기 때문에 따로 noti를 구현할 필요 없다.  

해당 프로젝트 Github 예제는 여기에 😊  
[sample-download-file](https://github.com/khs613/sample-download-file)  

&nbsp;  
&nbsp;  
[참고]  
<https://codechacha.com/ko/android-downloadmanager/>  
<https://developer.android.com/reference/android/app/DownloadManager>  
