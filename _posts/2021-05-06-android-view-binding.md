---
date: 2021-05-06
title: "[Android] ViewBinding"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
## 🍉 ViewBinding 📌

뷰 바인딩(ViewBinding)을 사용하면 뷰와 상호작용하는 코드를 쉽게 작성할 수 있다. 뷰 바인딩 속성이 활성화되면 각 XML 레이아웃 파일에 대한 바인딩 클래스가 자동 생성된다. `findViewById` 를 대체 한다.  
&nbsp;  

---

### 🎀 ViewBinding 설정  
- 모듈 활성화
build.gradle 파일에 다음과 같이 추가하자.  

```
android {
    ...
    viewBinding {
        enabled = true
    }
}
```
{: .notice--primary}  

&nbsp;  

### 🎀 ViewBinding 사용  
- 모듈에서 뷰 바인딩을 활성화 해줬다면, 각 XML 파일에 대해 바인딩 클래스가 생성된다.  
- 바인딩 클래스의 이름은 XML 파일의 이름을 카멜 표기법으로 변환되고 "Binding"이 추가된다.  
  - activity_main.xml 파일의 바인딩 클래스 이름은
  ActivityMainBinding 으로 변환!  
- getRoot() 메서드 포함  
모든 바인딩 클래스는 해당 레이아웃 파일의 루트뷰에 대한 직접 참조를 제공한다.  
- 액티비티에서 setContentView에 루트뷰 적용하기  

``` kotlin
private lateinit var binding: ActivityMainBinding

override fun onCreate(savedInstanceState: Bundle) {
  suuper.onCreate(savedInstanceState)
  binding = ActivityMainBinding.inflate(layoutflater)
  setContentView(binding.root)
}
```
{: .notice--primary}  

&nbsp;  

### 🎀 findViewById 와 차이점  
- Null safety  
뷰 직접 참조이므로 잘못된 ID로 Null pointer Exception 발생 위험 없다.  
- Type safety  
뷰 타입이 일치해서 Class Cast Exception 발생 안한다.  
&nbsp;  

### 🎀 DataBinding 과 차이점  
- 데이터 바인딩은 ``<layout>`` 태그를 사용한 레이아웃만 처리  
- 뷰 바인딩은 레이아웃 변수/표현식을 지원하지 않으므로 XML의 데이터와 레이아웃 바인딩 못한다.  
- 데이터 바인딩은 클래스를 생성할 때 루트뷰에 tag 삽입  
- 뷰 바인딩은 어노테이션 프로세싱 사용해서 더 빠르게 바인딩 클래스 생성  
- viewBinding 은 단순 작업에 적합하다!  

&nbsp;  
&nbsp;  
[참고]  
<https://developer.android.com/topic/libraries/view-binding?hl=ko>  
[https://charlezz.medium.com/view-binding-살펴보기-df3526d909a7](https://charlezz.medium.com/view-binding-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-df3526d909a7)  
<https://velog.io/@jaeyunn_15/AndroidViewBinding-vs-DataBinding>  
