---
date: 2021-04-05
title: "[Android] Live Template 사용하기"
categories: Android
tags:
    - android
toc: true
toc_sticky: true
---
#### Live Template 사용하기  
회사에서 프로젝트 협업을 하다보면 내가 만든 클래스나 파일에 대해 코멘트를 남겨야 할 때가 있다. 그때 함께 남겨야 할 정보를 자동으로 입력되는 기능을 찾다가 책임님께서 Live Template의 기능을 알려주셨는데, 굉장히 유용한 기능이다.  

##### Live Template  
코드 자동완성 기능이라고 생각하면 된다. 코드 작성 시 약어만 쳐도 자동완성을 해주는데, 사용자가 직접 추가/수정 할 수 있다. 자주 쓰는 코드나 코멘트를 추가해두면 저장한 단축키 만으로 자동완성 되므로 생산성을 향상 시켜준다.  

##### Android Studio에서 라이브 템플릿 추가하기  
1. Android Studio > preferences 이동  

2. Live Templates > 라이브 템플릿을 추가할 그룹 선택  
- 코멘트를 남기기 위해 추가 할 예정이니 AndroidComments 그룹 선택  
![livetemplate](/assets/img/post/2021-04-05-1/img_1.PNG)  

3. 오른쪽에 + 버튼 클릭 후 1.Live Template 선택  

4. template 구성  
- Abbreviation 설정 (키워드 입력)  
- Description 설명 추가  
- Template text 설정  
구성할 템플릿 내용을 작성한다. 변수 지정이 가능하다.  
![livetemplate](/assets/img/post/2021-04-05-1/img_2.PNG)  

5. 변수 지정 가능  
- 템플릿에 변수를 지정해서 변수를 자동으로 세팅하거나 사용자에게 입력하도록 설정할 수 있다.  
- `$변수명$` 과 같이 변수를 설정하면 Edit variables 버튼이 활성화 된다.  
- Edit variables 선택 후 각 변수에 해당하는 Expression을 적어준다.  
- `Skip if defined` 선택 시 자동으로 내용 적용.  
![livetemplate](/assets/img/post/2021-04-05-1/img_3.PNG)  



6. live template 사용  
- 키워드를 입력하면 추가한 템플릿이 자동완성 후보로 보여진다.  
- 또는 `ctrl + j` 단축키 입력 후 라이브 템플릿 목록에서 선택 후 사용하면 된다.  
![livetemplate](/assets/img/post/2021-04-05-1/img_4.PNG)  

코멘트 작성 시 사용했지만 반복되는 코드 작성에도 유용하게 사용 될 것 같다.  

&nbsp;  
&nbsp;  
[참고]  
<https://thinkerodeng.tistory.com/227>  
<https://blog.yena.io/studynote/2019/07/14/Android-Live-Templates.html>  
