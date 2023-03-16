---
date: 2023-01-15
title: "[Android] 로컬 Database Room 사용하기"
categories: Android
tags:
    - android
    - kotlin
    - room
toc: true
toc_sticky: true
---
## 🐋 Andorid Database Room 🐬

앱 내부에 로컬 데이터베이스를 이용하여 데이터를 저장하고 관리하는 방법으로 Room 이 있다. 안드로이드 developers 확인해보면 기존에 사용하던 SQLite에서 Room 라이브러리를 사용하라고 권장하고 있다.  
&nbsp;  

Room 라이브러리는 SQLite를 완벽히 활용하면서 원활한 데이터베이스 액세스가 가능하도록 SQLite에 추상화 계층을 제공한다.  
&nbsp;  

Room 라이브러리를 활용해서 오늘 할 일을 추가하는 예제를 만들어보겠다!  
&nbsp;  

---

### 📍 Room 사용시 이점  
- SQL 쿼리의 컴파일 시간 확인  
- 반복적이고 오류가 발생하기 쉬운 상용구 코드를 최소화하는 편의 주석  
- 간소화된 데이터베이스 이전 경로  
&nbsp;  

### 📍 build.gradle 환경 설정하기  
- dependency 추가  
- kotlin을 사용할 경우 annotationProcessor 대신 kapt 사용  

```
dependencies {
  implementation 'androidx.room:room-runtime:2.5.0'
  kapt 'androidx.room:room-compiler:2.5.0' // annotationProcessor
}
```
{: .notice--primary}  

- kapt 사용을 위해 plugin 추가  

```
plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
    id 'kotlin-kapt'
}
```
{: .notice--primary}  
&nbsp;  

### 📍 Room 구성요소  
- **Database** : 데이터베이스를 생성하고 데이터와 기본 연결을 위한 추상 클래스  
- **Entity** : 데이터베이스 테이블  
- **DAO(Data Access Object)** : 앱이 데이터베이스의 데이터에 접근할 수 있는 메소드를 정의해놓은 인터페이스  
<p align="center"><img src = "/assets/img/post/2023-01-15-1/img_1.png" width="70%"></p>  
&nbsp;  

### 📍 Entity 정의  
- 데이터베이스의 테이블 정보를 정의  
- `@Entity` 어노테이션 설정  
- 테이블이름은 클래스 네임이 default 값이니 따로 지정안해도 된다  
- 1개 이상의 식별할 수 있는 PrimaryKey 필요 (`@PrimaryKey` 어노테이션 사용)  
- autoGenerate = true 로 할 경우 key값 자동 생성  

``` kotlin  
@Entity(tableName = "table_todo")
data class TodoEntity(var title: String) {
    @PrimaryKey(autoGenerate = true)
    var id: Int = 0
}
```
{: .notice--primary}  
&nbsp;  

### 📍 DAO 정의  
- Room 에서는 데이터베이스에 직접 접근하지 않고, DAO 객체를 정의하여 접근  
- interface 혹은 Abstract class 로 정의  
- `@Dao` 어노테이션 설정  
- 추가, 업데이트, 삭제 기능을 작성함!  

``` kotlin  
@Dao
interface TodoDAO {
    @Query("SELECT * FROM table_todo")
    fun getAll(): List<TodoEntity>

    @Insert
    fun insertTodo(todo: TodoEntity)

    @Update
    fun updateTodo(todo: TodoEntity)

    @Delete
    fun deleteTodo(todo : TodoEntity)
}
```
{: .notice--primary}  
&nbsp;  

### 📍 Database 클래스 정의  
- 실제 데이터베이스에 연결을 위한 액세스 포인트!  
- `@Database` 어노테이션 설정  
- Entity의 구조 변경을 해야 할 때 이전과 구분해주기 위해 version을 관리  
- 서로 다른 스레드에서 데이터베이스를 한 번에 접근하는 것을 막기 위해 동기화 작업 필요  
- 데이터베이스 작업은 Main Thread 작동을 허용하지 않고 있다.  
- 그래서 Coroutine 사용해보자  

``` kotlin  
@Database(entities = [TodoEntity::class], version = 1)
abstract class TodoDatabase : RoomDatabase() {
    abstract fun todoDao(): TodoDAO

    companion object {
        private var instance: TodoDatabase? = null

        @Synchronized
        fun getInstance(context: Context): TodoDatabase? {
            if (instance == null)
                synchronized(TodoDatabase::class) {
                    instance = Room.databaseBuilder(
                        context.applicationContext,
                        TodoDatabase::class.java,
                        "todo.db"
                    ).build()
                }
                return instance
            }
        }
```
{: .notice--primary}  
&nbsp;  

### 📍 Database 사용하기  
- Todo 내용을 적은 후 추가버튼을 누르면 데이터를 화면에 뿌려주는 기능을 구현해보았다.  

``` kotlin  
  db = TodoDatabase.getInstance(this)

  CoroutineScope(Dispatchers.IO).launch { // 코루틴 사용 비동기로 실행
      binding.resultTextview.text = db!!.todoDao().getAll().toString()
  }

  binding.addButton.setOnClickListener {
      CoroutineScope(Dispatchers.Main).launch {
          val temp: Deferred<Boolean> = async(Dispatchers.IO) {
              db!!.todoDao().insertTodo(TodoEntity(binding.todoEdittext.text.toString()))
              binding.resultTextview.text = db!!.todoDao().getAll().toString()
              true
          }
          temp.await()
      }
  }
```
{: .notice--primary}  
&nbsp;  

### 📍 예제 화면  
<p align="left"><img src = "/assets/img/post/2023-01-15-1/img_2.png" width="50%"></p>  

&nbsp;  
&nbsp;  
[참고]  
<https://developer.android.com/training/data-storage/room?hl=ko>  
[모던 안드로이드 - 코틀린과 Jetpack 활용](https://www.inflearn.com/course/%EB%AA%A8%EB%8D%98-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%A0%9C%ED%8A%B8%ED%8C%A9)  
[https://velog.io/@soyoung-dev/AndroidKotlin-ROOM-Database-사용하기](https://velog.io/@soyoung-dev/AndroidKotlin-ROOM-Database-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)  
