---
date: 2021-01-29
title: "[Github] 깃허브 블로그 구글 검색 노출시키기"
categories: Github
tags:
    - github
    - sitemap
    - google
toc: true
toc_sticky: true
---
#### 깃허브 블로그 구글 검색 노출시키기

깃허브 블로그(Github.io)의 경우 검색엔진에 노출되지 않아 검색이 가능하도록 등록해줘야 한다. google, naver, daum 포털 사이트에 등록할 수 있는데, 우선 google 등록을 해보겠다.  
&nbsp;  

##### sitemap.xml 생성  
[sitemap](https://developers.google.com/search/docs/advanced/sitemaps/overview?hl=ko)은 사이트에 있는 페이지와 각종 파일들의 관계에 관한 정보를 제공하는 파일이다. sitemap을 구글에 등록해두면, 구글 검색엔진은 이 파일을 읽고 크롤링한다.  
 - _config.xml 파일에 url 속성에 내 블로그 url 이 들어가 있는지 확인  
 ( url : "https://khs613.github.io" )
 - sitemap.xml 파일을 github.io root 경로에 생성한다.  
 root 경로는 _config.xml 파일이 있는 폴더이다.  
 - sitemap.xml 작성  
 [sitemap 파일 링크](https://github.com/khs613/khs613.github.io/blob/master/sitemap.xml) 내용 복사해서 붙여넣자  

- github에 업로드 후 `blog주소/sitemap.xml` 로 접속해서 아래와 같이 정상적으로 나와야 한다.  
![sitemap](/assets/img/post/2021-01-29-1/img_2.png)  

##### robots.txt 생성
[robots.txt](https://developers.google.com/search/docs/advanced/robots/intro?hl=ko) 파일은 크롤러가 사이트에 요청할 수 있는 페이지 또는 요청할 수 없는 페이지를 알려 줄 수 있다.
- robots.xml 파일을 github.io root 경로에 생성한다.  
  root 경로는 _config.xml 파일이 있는 폴더이다.  

- robots.xml 작성  
[rebots 파일 링크](https://github.com/khs613/khs613.github.io/blob/master/robots.txt) 내용 복사해서 붙여넣기  
- 작성한 robots.txt 파일 github 업로드  


##### Google Search Console  
Google Search Console 에 블로그 사이트를 등록해서 구글 웹 크롤러가 내 블로그 사이트를 크롤링 할 수 있게 작업해준다.  

###### Google Search Console 사이트 등록  
- [Google Search Console](https://search.google.com/search-console/about) 접속한다.  
- 속성 유형 선택에서 Github blog 주소 입력하고 [계속] 선택  
![sitemap](/assets/img/post/2021-01-29-1/img_1.png)  
&nbsp;  
- 소유권 확인을 진행한다. 제공하는 html 파일을 다운받아서 파일을 github.io root 경로에 업로드 한 후에 확인을 누른다.
정상적으로 업로드가 되었다면 ``소유권이 자동으로 확인됨`` 이라는 창을 확인 할 수 있다.
![sitemap](/assets/img/post/2021-01-29-1/img_3.png)  
&nbsp;  

###### Google Search Console 에 sitemap 제출  
- Google Search Console 에 접속해서 왼쪽 메뉴 색인 > Sitemaps 선택한다.  
- 새 사이트맵 추가에 `sitemap.xml` 작성하고 제출한다.  
![sitemap](/assets/img/post/2021-01-29-1/img_4.png)  
&nbsp;  
- 이와중에 처음 제출할 때 잘못 기재한 부분이 있었는지 오류 3개가 떴다.  
![sitemap](/assets/img/post/2021-01-29-1/img_5.png)  
&nbsp;  
- sitemap.xml 파일을 수정해주고, github에 업로드 한 후 다시 제출했더니 성공으로 상태가 변경되었다. (반영 시간이 굉장히 느린듯 싶다. 수정하고 바로 제출할때는 안되더니 나중에 하니까 성공)  
![sitemap](/assets/img/post/2021-01-29-1/img_6.png)  
&nbsp;  

###### 구글에서 사이트 검색  
모든 설정이 끝났으면 실제로 구글에 검색해보자. 제출하고 곧바로 반영이 안되고 1-2시간 혹은 며칠 걸리는 경우도 있는 것 같다. 이후에 확인해 보도록!  

&nbsp;  
&nbsp;  
[참고]  
<http://jinyongjeong.github.io/2017/01/13/blog_make_searched/>  
<https://wayhome25.github.io/etc/2017/02/20/google-search-sitemap-jekyll/>  
