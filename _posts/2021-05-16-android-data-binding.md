---
date: 2021-05-16
title: "[Android] DataBinding"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
#### DataBinding

데이터 바인딩(DataBinding)은 UI 요소와 데이터를 프로그래밍적 방식으로 연결하지 않고, 선언적 방식으로 결합할 수 있게 도와주는 라이브러리이다.  
프로그래밍적 방식이라 하면 기존에 코드 내에서 UI 요소를 가져와 `findViewById` 로 데이터와 결합해준 후 데이터를 할당하는 방식이다. 선언적 형식은 코드 내에서 UI 요소를 호출할 필요 없이 레이아웃 파일(xml)에서 직접 할당해주는 방식이다.  

##### DataBinding 장점  
- 데이터와 UI 요소를 연결하기 위한 코드 최소화  
- `findViewById` 를 호출하지 않아도, 자동으로 xml에 view를 생성  
- RecyclerView 사용 시 item 자동으로 set  
- data 변경 시 자동으로 view 변경  
- 코드 가독성이 좋아지고, 상대적으로 코드량 감소  
- MVP / MVVM 패턴 구현에 유용  

다만, 클래스 파일이 많이 생기고, 빌드 속도가 느려지는 단점도 존재하기 때문에 단독으로 사용하기 보다는 아키텍처 패턴과 함께 사용할 때 최대한 활용할 수 있다.  

##### DataBinding 설정  
- 모듈 활성화
build.gradle 파일에 다음과 같이 추가하자.  

```
android {
    ...
    dataBinding {
        enabled = true
    }
}
```
{: .notice--primary}  

#### DataBinding 사용  
##### 1. xml 파일에 <layout> 태그 작성  
- dataBinding을 사용하는 xml 파일의 루트 레이아웃을 `<layout>` 태그로 감싼다.  

``` xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android">
...
</layout>
```
{: .notice--primary}  

##### 2. `<data>` 태그와 `<variable>` 태그 사용  
- 레이아웃의 뷰에 연결할 변수가 있을 경우 사용된다.  
- 연결할 data 객체를 만들어 주자.  

``` kotlin
data class User (
    val name: String,
    val age: Int
)
```
{: .notice--primary}  

- `@{}` 구문을 사용하여 레이아웃 컴포넌트에 변수를 할당한다.  

``` xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android">

    <data>
        <variable
            name="user"
            type="com.khs.DataBinding.User" />
    </data>
    ...
    <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@{user.name}" />
```
{: .notice--primary}  

##### 3. 바인딩 객체 만들기  
- 레이아웃 파일에 DataBinding을 적용하면 자동으로 바인딩 클래스가 생성 된다.  
- 뷰바인딩 포스팅에도 언급한 카멜 표기법으로 변환된 이름으로 생성  
  - activity_main.xml 파일의 바인딩 클래스 이름은 ActivityMainBinding 으로 변환!  
- 기존의 setContentView() 함수를 <b>DataBindingUtil.setContentView()</b>로 변경한다.  

``` kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = DataBindingUtil.setContentView(
            this,
            R.layout.activity_main
        )

        binding.user = User("홍길동", 20)
    }
}
```
{: .notice--primary}  
&nbsp;  
기본적으로 dataBinding 설정과 사용법을 살펴보았다. 다음에는 RecyclerView에서 dataBinding를 사용해 봐야지.  

&nbsp;  
&nbsp;  
[참고]  
<https://velog.io/@yxnsx/Android-DataBinding>  
