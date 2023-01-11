---
date: 2022-11-15
title: "[Android] Koin 사용하기"
categories: Android
tags:
    - android
    - koin
    - kotlin
toc: true
toc_sticky: true
---
#### Koin 사용하기

공부해야지 백만번은 마음 먹은 것 같은데, 이제서야 들여다보는 DI (Dependency Injection)  
Koin은 코틀린 개발자를 위해 개발된 실용적이고 가벼운 의존성 주입 프레임워크다. 의존성 주입 프레임워크는 대표적으로 `Dagger`, `Hilt`, `Koin` 등이 있는데, `Koin` 은 가장 낮은 러닝 커브를 자랑하여 의존성 주입에 입문하기 좋은 프레임워크!  

의존성 주입은 필요한 객체를 직접 생성하지 않고 외부로부터 객체를 넘겨 받아서 사용하는것을 뜻한다 어떤 Activity나 Fragment에서 객체를 생성하는지에 따라 Context가 계속 바뀌기 때문에 같은 클래스 타입 객체임에도 다르게 동작할 수 있다. 외부에서 객체를 생성하고 이 생성된 객체를 Activity나 Fragment에 주입 받아 사용하면 Context의 영향을 받지 않고도 공통으로 재사용할 수 있는 객체를 구현하게 된다.  
설명만으로는 어떤 식으로 사용해야하는 건지 감이 잘 오지 않아서 정리된 블로그들을 통해서 Koin을 적용하는 과정을 따라해봤다.  
&nbsp;  

---

##### DI 사용시 이점  
- 코드의 가독성과 재사용성을 높여준다.  
- 단위 테스트 용이  
- 객체 간의 의존(종속) 관계를 직접 설정할 수 있음  
- 객체 간의 결합도를 낮춰 줌  
&nbsp;  

##### Koin 사용 시 알아둬야 할 키워드  
- module : 주입 받고자 하는 객체를 모듈로 만들어 선언    
- single : 앱이 실행되는 동안 계속 유지되는 싱글톤 객체를 생성  
- factory : 요청할 때마다 매번 새로운 객체 생성  
- get() : 컴포넌트 내에서 알맞은 의존성을 주입 받음  
&nbsp;  

##### dependency 추가  

```
dependencies {
    implementation 'org.koin:koin-androidx-viewmodel:2.1.5'
}
```
{: .notice--primary}  
&nbsp;  

##### 모듈 선언  
1. 샘플 클래스 생성  

``` kotlin
class SampleRepository() {
    val sampleData = "Sample Repository"
}

class SampleController(val repository: SampleRepository) {
    fun printSampleData() {
        Log.d("Print sample data", repository.sampleData)
    }
}

class SampleViewModel : ViewModel() {
    private var _isLoading = MutableLiveData<Boolean>()
    val isLoading: LiveData<Boolean> = _isLoading
}
```
{: .notice--primary}  

2. 모듈로 선언하여 변수에 저장  

``` kotlin
val appModule = module {
    single { SampleRepository() }
    factory { SampleController(get()) }
}

val viewModelModule = module {
    viewModel { SampleViewModel() }
}
```
{: .notice--primary}  

위에서 언급했던 Koin에서 알아둬야 할 키워드를 대입해보자면,
- `single` 컨테이너 내에서 단 한번만 생성되고  
- `factory` 컨테이너 내에서 요청 시점마다 새로운 객체 생성  
- `get()` 컨테이너 내에서 알맞은 의존성을 주입  
- `viewModel` ViewModel의 경우는 `viewModel` 키워드로 선언  
&nbsp;  

##### 모듈 등록  

``` kotlin
class InquiryApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        startKoin {
            androidLogger()
            androidContext(this@InquiryApplication)
            modules(appModule)
            modules(viewModelModule)
        }
    }
}
```
{: .notice--primary}  

- `startKoin` 을 호출해서 선언한 모듈 변수를 넘겨준다.  
- `androidLogger()` : AndroidLogger를 Koin logger로 사용  
- `androidContext()` : 해당 안드로이드 context 사용  
- `modules()` : 사용할 모듈 등록  
- Application 클래스 생성 후 꼭 `AndroidManifest.xml`에 등록해야 함!  

```
<application
    android:name=".InquiryApplication"
    ...
}
```
{: .notice--primary}  

&nbsp;  

##### 의존성 주입  
- `inject()` 키워드를 사용하여 의존성을 주입  
- ViewModel의 경우 `viewModel()` 사용  
- 사용하고자 하는 Activity 클래스에서 주입하면 된다.  

``` kotlin
class SampleActivity : AppCompatActivity() {

    val controller: SampleController by inject()
    val viewModel: SampleViewModel by viewModel()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate()
    }
}
```
{: .notice--primary}  


&nbsp;  
&nbsp;  
[참고]  
<https://salix97.tistory.com/265>  
<https://velog.io/@hoyaho/Koin>  
<https://spoqa.github.io/2020/11/02/android-dependency-injection-with-koin.html>  
