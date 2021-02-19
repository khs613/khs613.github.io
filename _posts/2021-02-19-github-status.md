---
date: 2021-02-19
title: "[Github] Git 영역과 파일 상태"
categories: Github
tags:
    - github
toc: true
toc_sticky: true
---
#### 깃(Git) 영역과 파일 상태, 스냅샷  
Git에서 어떻게 파일을 관리하고 동작하는지 공부해 보았다. git 영역과 데이터 저장 방법, 파일 상태에 대해 알아보자.  
&nbsp;  

#### Snapshot (스냅샷)  
- git에서 데이터를 저장하는 방식.  
- git이 다른 버전 관리 도구와 다른 점은 스냅샷 방식을 이용한다는 것이다.  
- git은 저장소의 파일 시스템 전체를 스냅샷으로 취급한다. 커밋 시점의 저장소 상태가 하나의 버전이 된다. 파일이 변경되지 않았다면 Git은 파일을 새로 저장하지 않고 링크만 저장한다.  
- (파일을 복사하는 방식으로 수정본을 관리하면 같은 내용을 반복해서 저장하기에 많은 용량을 차지하고, 수정된 부분을 일일이 찾게되면 검색 시 불편함이 있다.)  
&nbsp;  

#### 깃(Git) 세 가지 영역  
---

##### Working Directory (작업 영역)
- working tree (워킹트리) 라고도 한다.  
- 실제 작업을 하는 프로젝트 디렉토리  

##### Staging Area (Index)  
- working directory에서 repository로 정보가 저장되기 전 준비 영역  
- `git add` 한 파일들이 존재하는 영역  
- `git commit` 으로 index 에서 repository로 저장된다.  

##### Repository (.git directory)  
- 작업 디렉토리의 변경 이력들이 저장되어 있는 영역  

![github](/assets/img/post/2021-02-19-1/img_1.png)  
<span style="color:gray">(사진 출처 : [https://git-scm.com/book/ko/v2/시작하기-Git-기초](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88))</span>  

#### 깃(Git) 파일 상태(status)  
---
git은 먼저 추적 관리 여부에 따라 크게 두 가지 상태로 나뉜다.  

- Untracked : git이 추적 및 관리하지 않는 상태  
작업 디렉토리에 존재하는 파일이라고 해서 모두 git이 관리하는 파일은 아니다. Untracked 파일은 수정되거나 삭제가 되어도 git에서 신경쓰지 않는다.  

- Tracked : git이 추적 및 관리해주는 상태  
Tracked 상태인 파일은 최소한 한번은 `git add` 명령어를 통해 Staging area에 포함되거나, `commit`을 통해 git 디렉터리에 저장된 파일이다.  
&nbsp;  
그리고 Tracked 상태에서는 파일 변경 여부에 따른 세 가지 상태로 나뉜다.  

##### unmodified  
- 파일이 수정되지 않은 상태 (파일이 최근에 저장한 상태 그대로인)  

##### modified  
- 파일이 수정된 상태  
- `git add` 명령어를 실행하면 staged 상태로 올린다.  

##### staged  
- `git commit` 명령어로 저장소에 기록 예정인 상태를 뜻한다.  

![github](/assets/img/post/2021-02-19-1/img_2.png)  
<span style="color:gray">(사진 출처 : [https://git-scm.com/book/ko/v2/Git의-기초-수정하고-저장소에-저장하기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0))</span>  

&nbsp;  
&nbsp;  
[참고]  
<https://thebook.io/080212/ch04/04/02/>  
