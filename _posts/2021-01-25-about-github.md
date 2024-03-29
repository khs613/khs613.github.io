---
date: 2021-01-25
title: "[Github] 깃허브(Github)에 대하여"
categories: Github
tags:
    - github
toc: true
toc_sticky: true
---
## 👻 깃허브에 대하여 🤠

위키백과에 따르면, [깃허브](https://ko.wikipedia.org/wiki/%EA%B9%83%ED%97%88%EB%B8%8C)(Github)는 분산 버전 관리 툴인 깃(Git)을 사용하는 프로젝트를 지원하는 웹호스팅 서비스이다.
&nbsp;  

버전 관리와 협업을 위한 코드 호스팅 플랫폼이다. 언제 어디서나 협업 프로젝트를 쉽게 진행할 수 있도록 돕는 것이다.  
&nbsp;  

---

### 👉 로컬 저장소, 원격 저장소
저장소는 파일이나 디렉토리를 저장하는 장소이다. 파일이나 디렉토리 등을 저장소의 관리하에 두는 것으로, 변경 내역을 기록하고 변경 이력 관리 가능하다.
  * 로컬 저장소 : 자신의 컴퓨터에 있는 저장소
  * 원격 저장소 : 서버와 같은 네트워크에 있는 저장소
  * 협업을 할 때, 기본적으로 로컬 저장소에서 작업을 수행하고 그 결과를 원격 저장소에 저장
&nbsp;  

### 👉 브랜치(branch)
브랜치란 독립적으로 어떤 작업을 진행하기 위한 개념이다. 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있다.  
이러게 만들어진 브랜치는 다른 브랜치와 병합(Merge)함으로써, 작업한 내용을 다시 새로운 하나의 브랜치로 모을 수 있다. 저장소를 처음 만들면, Git은 바로 'master'라는 이름의 브랜치를 만들어 준다.
&nbsp;  

### 👉 작업한 파일을 올려보자
깃허브에 작업한 파일을 올릴 때는 기본적으로 add, commit, push를 사용한다.

1. <b>git add .</b>  
위 명령문을 입력하면 현재까지 작업중이던 파일들을 모두 추가해 깃허브에 올리기 위한 staging area에 올린다.  
&nbsp;  
2. <b>git commit -m "commit message"</b>  
![예시](/assets/img/post/2021-01-25-2/img_1.png)  
staging area에 올린 파일들을 위 명령어로 commit 하면 깃허브에 올릴 준비가 끝난다. commit message는 웬만하면 써주는게 좋다. 나중에 push 한 것을 되돌리고 싶을 때, 해당 commit을 찾아 push해야 하기 때문이다.  
그리고 협업할 때 어떤 수정 사항이 있는지, 추가된 부분은 무엇인지 기재해두면 서로 일하기 편하기 때문에...!  
&nbsp;  
3. <b>git push origin master</b>  
![예시](/assets/img/post/2021-01-25-2/img_2.png)  
origin은 처음 Git 설정 시 현재 원격 저장소(remote repository)에 붙여준 이름이다.  

&nbsp;  
이후에 깃허브에 commit 이력이 남아있는 것을 확인할 수 있다.  
우선은 기본적인 commit 방법을 알아 봤다. 나중에 더 심화해서 알아보도록 해야지.  


&nbsp;  
&nbsp;  
[출처]  
<https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html>  
<https://tagilog.tistory.com/377>  
<https://ninano1109.tistory.com/2>
