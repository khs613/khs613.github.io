---
date: 2021-02-19
title: "[Github] Git 명령어 모음"
categories: Github
tags:
    - github
toc: true
toc_sticky: true
---
## 🛝 깃(Git) 명령어로 알아보는 기초 🎹

git 저장소를 사용함에 있어서 기초적인 내용은 알아야 할 것 같아 명령어를 통해 공부해보고자 한다. 이해한 내용을 간단하게 정리해서 작성한 글이다.  
&nbsp;  

---

##### $ git init  
- git 저장소 초기화. 명령어를 입력하기 전까지는 일반 디렉토리였지만, 초기화를 시키면 해당 디렉토리를 로컬 깃 저장소로 등록해 준다.  
- 해당 명령어를 입력 후에 추가적인 git 명령어 줄 수 있다.  
&nbsp;  

##### $ git clone <URL>  
- 원격저장소로 부터 프로젝트를 복제하는 것을 말한다.  
- 저장소를 clone 하면 'origin' 이라는 리모트 저장소가 자동으로 등록된다.  
&nbsp;  

##### $ git remote  
- 현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다.  
- `-v` 옵션을 주면 단축이름과 URL을 함께 볼 수 있다.  
&nbsp;  

##### $ git config  
- git 사용 환경 설정 확인하고 변경할 수 있다.  
&nbsp;  

##### $ git status  
- 파일들의 가능한 상태를 확인할 수 있다.  
- 작업 디렉토리(working directory)와 스테이징 영역(staging area)의 상태를 확인하기 위해 사용한다.  
&nbsp;  

##### $ git add  
- 작업 디렉토리 상의 변경 내용을 스테이징 영역에 추가하기 위해 사용하는 명령어.  

$ git add <파일/디렉토리 경로>
{: .notice--primary}  
변경 내용의 일부만 스테이징 영역에 넘기고 싶을 때 디렉토리의 경로를 인자로 넘긴다.  

$ git add .
{: .notice--primary}  
현재 디렉토리의 모든 변경 내용을 스테이징 영역으로 넘기고 싶을 때 `.` 인자로 넘긴다. (상위 디렉토리의 변경 내용은 포함하지 않음)  

$ git add -A
{: .notice--primary}  
작업 디렉토리 상에 어디에 위치하든 항상 동일하게 모든 변경 내용을 스테이징으로 넘긴다.  

$ git add -p
{: .notice--primary}  
각 변경 사항을 터미널에서 직접 눈으로 확인하면서 스테이징 영역으로 넘기거나 또는 제외할 수 있다.  
&nbsp;  

##### $ git commit -m "commit message"
- 파일 및 폴더의 추가/변경 사항을 저장소에 기록한다.  
- 인덱스(staging area)에 등록되어 있는 파일 상태를 기록한다.  
&nbsp;  

##### $ git push <저장소명> <브랜치명>  
- 로컬 저장소에서 남겨놓은 파일 변경 이력을 원격 저장소로 전송한다.  
- `-u` 옵션을 사용하면 최초 한 번만 저장소명과 브랜치명을 입력하고 이후에 생략 가능하다.  
&nbsp;  

##### pull vs fetch  
1. $ git pull  
- 원격저장소로 부터 변경된 내용을 가지고 온 후 병합(merge)  
- pull = fetch + merge 와 같은 의미!  

2. $ git fetch  
- 원격저장소로 부터 변경된 내용을 가지고 온 후 병합 x  
- 변경된 내역을 가지고 온 후 검토 후에 merge 할 수 있어서 충돌 방지  
&nbsp;  

##### $ git branch <브랜치명>  
- 브랜치를 생성하는 명령어  
- master 브랜치에서 <브랜치명> 이라는 브랜치를 생성한다.  
&nbsp;  

##### $ git checkout <브랜치명>  
- 현재 master 브랜치에서 <브랜치명> 으로 이동하기 위한 명령어  
- `b` 옵션을 사용하면 브랜치 생성과 체크아웃을 한번에 할 수 있다.  
&nbsp;  

##### $ git merge <브랜치명>  
- 브랜치를 병합하는 명령어  
- 협업 과정에서 같은 이름의 파일 안에 수정한 부분이 겹칠 때 충돌(conflit)이 발생 할 수 있다.  
&nbsp;  

##### $ git rebase  
- 브랜치를 병합하는 명령어로 merge와 같은 기능이지만,  
- merge의 경우 병합 할 브랜치에서 기록한 모든 commit이 master의 commit으로 기록된다.  
- rebase의 경우 작업 중 남겼던 commmit 중 불필요한 것들을 생략시키고 필요한 commit만 남겨서 master 병합이 가능하다.  
- `-i`는 interactive라는 옵션이다. 해당 옵션을 사용하면 중간에 낀 커밋 메세지를 수정할 수 있다.  

&nbsp;  
&nbsp;  
[참고]  
[https://velog.io/@delilah/GitHub-Git-명령어-모음](https://velog.io/@delilah/GitHub-Git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EB%AA%A8%EC%9D%8C)  
<https://www.daleseo.com/git-push/>  
<https://mylko72.gitbooks.io/git/content/branch/checkout.html>  
[https://flyingsquirrel.medium.com/git-rebase-하는-방법-ce6816fa859d](https://flyingsquirrel.medium.com/git-rebase-%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-ce6816fa859d)  
