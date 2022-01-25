---
title: 
categories:
- blog
tags:
- blog
last_modified_at:
---


오늘은 블로그에 다음과 같이 sidebar를 추가해보도록 하겠습니다. 

![image](https://user-images.githubusercontent.com/79133602/150911925-ffc9333e-25c9-4c46-aeec-d11e84014f48.png)
<br/>
❗ 해당글은 jekyll minimal-mistakes를 기준으로 작성됐습니다. 

<br/>
# 1. categories 등록

 sidebar 클릭시 해당 메뉴 이름과 같은 catergory인 글 목록만 나타나는 기능을 구현 하려면 
 먼저 게시물의 categories 속성값을 넣어주셔야 합니다. 아래처럼 직접 게시글 파일의 front matter에 지정해주셔도 되고

![image](https://user-images.githubusercontent.com/79133602/150912269-2bb7d09e-3b02-4e61-8b88-669ec4405440.png)

아예 디렉토리에 카테고리 이름으로 폴더를 만들어 자동으로 카테고리로 만들 수도 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/150912515-3395a828-f384-4380-916e-a4783ce6c0c1.png)

이경우엔 카테고리 폴더에 _posts 폴더를_ 또 만들고 그안에 게시글을 올리면 됩니다. 

![image](https://user-images.githubusercontent.com/79133602/150912826-55636f21-25b1-4087-8676-fd518e6f5c1f.png)

<br/><br/>
# 2. navigation.yml 수정

이제 sidebar를 만들 건데요. _data 폴더의_ navigation.yml 파일에 새로운 key 값을 추가하고 그 아래 title엔 메뉴명을
url엔 permalinnk값이 될 값을 넣어줍니다. 만약 메뉴안에 하위 메뉴를 넣고 싶다면 title: 메뉴명 아래 Childeren: 속성을 사용해주세요. 

```
sidebar-list:
  - title: Programming
    children:
      - title: "Install"
        url: /install/
      - title: "Java"
        url: /java/
      - title: "JS"
        url: /js/
      - title: "DB"
        url: /db/
      - title: "React"
        url: /react/
      - title: "FrontEnd"
        url: /frontend/
      - title: "Error"
        url: /error/
      - title: "Git"
        url: /git/

  - title: "Blog"
    url: /blog/

  - title: "ETC"
    url: /etc/


  - title: Project
    children:
      - title: "shoppingMall"
        url: https://bellasimi.github.io/shoppingMall/
```
<br/>
# ❗ 주의점

1. depth를 명확히 해주세요. key, title, url, childeren 속성을 전부 같은 깊이에 쓰면 인식 못해요.

2. title 값은 ""안에 써주시되 Children속성 위 title은 ""없이 써주세요.

3. url엔 "" 붙이지 않습니다. 사이트 연결시 사이트 주소를 url에 넣어주세요.

4. main key 데이터 아래에 작성해주세요. main key에 입력한 값은 우측상단 nav입니다. 삭제하거나 주석처리하시면 nav가 사라져요! 

<br/><br/>
# 3. sidebar 등록

sidebar를 블로그에 항상 나오게 하려면  _config.yml파일을_ 바꿔주시면 됩니다.
defaults 키 값에 아래 값을 추가해주세요.

```
# Defaults
defaults:
  # main
  - scope:
      path: ""
    values:
      author_profile: true
      sidebar: 
        nav: "sidebar-list"
```

sidebar의 <span style="color:red; font-weight:bold">nav값</span>엔 아까 navigation.yml에서 작성한 
<span style="color:red; font-weight:bold">sidebar의 key값</span>을 넣습니다. 

<br/>
# ❗ 주의점

author_prof1ile이 true여야 sidebar가 나옵니다! false면 sidebar 속성값이 있어도 안나오니 주의해주세요. 

<br/><br/>
# 4. page 만들고 permalink 부여


_pages 폴더에_ 가서 sidebar 메뉴 클릭시 나올 페이지를 만들어 줍니다. 
전 /java/라는 url접속시 archive 레이아웃 html이 뜨고 해당 페이지에 title로 Java가 나오는 category-java.md를 만들었습니다. 

```
---
title: "Java"
permalink: /java/
layout: archive
---

{% assign posts = site.categories.java %}
{% for post in posts %}
	{% include archive-single.html type=page.entries_layout %}
{% endfor%}
```

assign posts = site.categories.java 카테고리가 java인 post들을 posts에 할당하고, 해당 카테고리의 post들을 entries_layout을 써서 리스트로 출력합니다.

<br/><br/>
# 끝 

모든 파일을 push한 뒤 sidebar의 java메뉴를 클릭하면 java 카테고리만 모아둔 category-java페이지가 /java/ url로 잘뜨는 것을 볼 수 있습니다.

![image](https://user-images.githubusercontent.com/79133602/150917468-5c362ea7-8abe-44d7-a37f-de2b26221612.png)

이런식으로 다른 sidebar의 페이지를 만들면 블로그 sidebar 기능 완성입니다.

<br/><br/><br/>
# 참고

🖥 [ minimal-mistakes menual ] ( https://mmistakes.github.io/minimal-mistakes/docs/layouts/#custom-sidebar-navigation-menu )

🖥 [ jekyll 같은 카테고리만 모아두는 페이지 생성 ] ( https://ansohxxn.github.io/blog/category/#2%EF%B8%8F%E2%83%A3-%EA%B0%99%EC%9D%80-%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC%EB%A7%8C-%EB%AA%A8%EC%95%84%EB%91%90%EB%8A%94-%ED%8E%98%EC%9D%B4%EC%A7%80)

🖥 [ gitpage 블로그 만들기 ] ( https://seungwubaek.github.io/blog/post_1/#page-title )
