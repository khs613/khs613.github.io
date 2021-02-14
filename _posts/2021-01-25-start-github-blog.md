---
date: 2021-01-25
title: "깃허브 블로그 시작하기 (Github Blog)"
categories: Github
tags:
    - github
    - blog
toc: true
toc_sticky: true
---
#### 깃허브 블로그 시작하기

회사에서 거북이 TortoiseSVN 를 사용하고 있기 때문에 평소에 Github를 사용해보지 않았다. 그래서 그런지 모든 과정이 너무 어렵다. 블로그는 Tistory, Medium 등과 같은 다른 걸 써볼까 하다가.. 깃허브를 배워볼 겸 고생 한 번 해보자 싶어서 Github Blog 결정!  
공부하고자 시작한 블로그이기 때문에, 간단한 필기 수준으로 보면 될 것 같다.  
&nbsp;  

##### 깃허브 블로그 구축 과정
1. 깃허브 가입
   * [깃허브 링크](https://github.com/)
2. Repository 생성
   * Repository 명은 <b>[본인아이디]</b>.github.io 로 설정
3. Jekyll 테마 선택
   * [Jekyll 테마 링크](http://jekyllthemes.org/)
   * 내가 선택한 테마는 [minimal mistakes](https://github.com/mmistakes/minimal-mistakes)
   * 테마 종류가 굉장히 많아서 오히려 선택하기 어려웠다. 그래서 블로그에서 추천하는 테마 중 한 개를 택했다. 깔끔해서 좋다!
4. _config.yml 변경
   * _config.yml 파일을 사용자에 맞게 설정
   ![예시](/assets/img/post/2021-01-25-1/img_1.png)
   파일을 보면 사이트 설정에 관한 내용이다. 내 정보를 기입하면 되는데, 다른 테마보다 더 많은 정보가 포함되어 있다. 조만간 해당 테마에 대해서도 공부를 더 해봐야 할 것 같다.
5. 포스팅 해보기
   * _post 폴더 안에 YYYY-MM-DD-[제목].md 형식으로 파일 생성 한 후 add, commit, push 과정 거치며 포스팅

&nbsp;  
여기까지 과정을 보면 굉장히 간단하다고(?) 생각할 수 있는데, 나는 이 과정만 며칠이 소요됐다. 하나 하나 쉬운게 없었고...  
막상 글로 쓰려고 하니 도저히 정리가 되지 않아 간단하게만 나열해 봤다. 남에게 지식을 전달하는 것도 굉장히 어려운 일이다.  

&nbsp;  
&nbsp;  
[참고]  
<https://zoomkoding.github.io/gitblog/2019/08/15/git-blog-1.html>  
<https://dreamgonfly.github.io/blog/jekyll-remote-theme/>
