---
date: 2021-02-19
title: "[Android] Retrofit 사용하기 (GET 방식)"
categories: Android
tags:
    - android
    - retrofit
toc: true
toc_sticky: true
---
#### Retrofit 사용하기  
Retrofit은 서버와 통신할 때 사용하는 Square 사의 라이브러리이다.  
공식 페이지는 [여기](https://square.github.io/retrofit/)  

##### Retrofit 이란?
- REST API 통신을 위해 구현되었다.  
- `OKHttp` 라이브러리의 상위 구현체
- retrofit은 OKHttp를 네트워크 계층으로 활용하고 그 위체 구축되었다.  

##### Retrofit 장점  
- 빠른 성능 (AsyncTask의 3~10배의 성능차이)
- Annotation 사용으로 코드 가독성 뛰어남  
- 반복된 작업을 라이브러리에 넘겨서 처리하므로 간단한 구현  

##### 구성요소  
- DTO(POJO)  
'Data Transfer Object', 'Plain Old Java Object' 형태의 모델  
JSON 타입변환에 사용  
- Interface  
사용할 HTTP 동작들을 정의해놓은 인터페이스  
- Retrofit.Builder 클래스  
Interface를 사용할 인스턴스로, baseUrl / Converter 설정  

#### Retrofit 사용방법  
이번 예제는 서버에서 URL 데이터를 가져와서 리스트에 뿌려주려고 한다. http 통신은 GET 방법을 사용 할 것이고, 받을 데이터가 URL 데이터 뿐이라 따로 DTO 모델은 구성하지 않았다. 다음에 POST 방식을 사용해서 DTO 모델까지 같이 구성해보는 걸로.   

##### Gradle 추가  
- `build.gralde`에 다음과 같이 Retrofit 라이브러리 추가  

```
dependencies {
	...
    implementation 'com.squareup.retrofit2:converter-gson:2.6.2'
    implementation 'com.squareup.retrofit2:retrofit:2.6.0'
}
```

##### 인터넷 권한 설정  
- 매니페스트 파일에 인터넷 권한 추가  

```
<uses-permission android:name="android.permission.INTERNET"/>
```
{: .notice--primary}  

##### interface 정의  
- RetrofitAPI 인터페이스 생성  

``` java
package com.khs.sample_download_file.server;

import okhttp3.ResponseBody;
import retrofit2.Call;
import retrofit2.http.GET;

public interface RetrofitAPI {
    String MOCK_SERVER_URL	= "https://f3a07bac-0217-476a-af05-330554d63fda.mock.pstmn.io/"; // 통신 할 서버 baseUrl

    @GET("downloads")	// 전체 URL 에서 URL을 제외한 End Point를 적어준다.
    Call<ResponseBody>getURL();
}
```
{: .notice--primary}  

- 사용 할 메서드를 정의한다.  
- Server API에 맞게 메서드 정의해주는데, @Header/@Query/@Field 등의 정보를 알맞게 작성해주면 된다.  
- 이번 예제에서는 아주 간단하게 서버 데이터만 받아오는 거라 헤더나 쿼리와 같은 인자는 따로 작성하지 않았다.  
- End Point?  
<img src = "/assets/img/post/2021-02-23-1/img_1.png" width="60%">  

##### Retrofit 인스턴스 생성  
- RetrofitClient 클래스  

``` java
package com.khs.sample_download_file.server;

import retrofit2.Retrofit;
import retrofit2.converter.gson.GsonConverterFactory;

public class RetrofitClient {
    Retrofit retrofit = new Retrofit.Builder()
            .baseUrl(RetrofitAPI.MOCK_SERVER_URL) // baseUrl 등록
            .addConverterFactory(GsonConverterFactory.create()) // JSON을 변환해줄 Gson 변환기 등록
            .build();

    public RetrofitAPI retrofitAPI = retrofit.create(RetrofitAPI.class);
}
```
{: .notice--primary}  

- RetrofitClient 클래스 사용해서 통신 작업 실행  

``` java
private void retrofitConnection() {
        RetrofitClient retrofitClient = new RetrofitClient();
        Call<ResponseBody> call = retrofitClient.retrofitAPI.getURL();
        call.enqueue(new Callback<ResponseBody>() {
            @Override
            public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
                ResponseBody responseBody = response.body();
                try {
                    String result = responseBody.string();
                    if (jsonParseResult(result)) {
                      // 정상적으로 통신 성공한 경우
                    }
                } catch (IOException e) {

                }
            }

            @Override
            public void onFailure(Call<ResponseBody> call, Throwable t) {
              // 통신 실패
            }
        });
    }
```
{: .notice--primary}  

정상적으로 통신이 완료되면 onResponse 콜백을 통해 서버의 데이터를 받을 수 있다. 예제 프로젝트에서는 json을 통해 데이터를 파싱하였는데, 지정한 DTO 클래스가 있다면 자동으로 파싱해 줄 것이다. 다음 예제 때 꼭 DTO 클래스로 테스트를 해봐야 겠다.  

해당 프로젝트 예제는 여기에!  
[sample-download-file](https://github.com/khs613/sample-download-file)  

&nbsp;  
&nbsp;  
[참고]  
<https://jaejong.tistory.com/33>  
[https://ppizil.tistory.com/entry/Retrofit2-기본-사용법](https://ppizil.tistory.com/entry/Retrofit2-%EA%B8%B0%EB%B3%B8-%EC%82%AC%EC%9A%A9%EB%B2%95)
