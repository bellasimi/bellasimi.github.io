---
title: 
categories:
- blog
tags:
- blog
last_modified_at:
---

github에 올린 페이지에 댓글달기 기능을 추가하고 싶다면, utterance를 사용하시면 됩니다. 
utterances는 github의 이슈를 만드는 방식으로 댓글을 생성합니다. 
<br/>
# 사용법

먼저 [ utterances git 페이지 ]( https://github.com/apps/utterances )로 이동해주세요. 
<br/><br/>
## 1. utterances 연동

이 단계에서 github의 issue를 만들 수 있도록 연동을 하고 권한부여를 해줍니다.

![image](https://user-images.githubusercontent.com/79133602/150093725-68584473-b15e-4b42-9ab0-1514c3a77432.png)

install 버튼을 클릭하고 연동해줄 자신의 레포지토리를 선택합니다.

![image](https://user-images.githubusercontent.com/79133602/150093898-76165c8b-ae4d-461b-9be4-2540e7862e2a.png)

전 블로그만 연동할거라 bellasimi.github.io만 선택했습니다. 다시 install 버튼을 클릭하면 비번입력창이 뜨고 비번 확인 후 
스크립트 생성페이지로 이동합니다. 

<br/><br/>
## 2. 스크립트 생성

생성된 github 이슈를 화면에 표시하기 위해 utterances 스크립트를 생성해야 되는데요. 

![image](https://user-images.githubusercontent.com/79133602/150094852-255c3133-d419-4581-b279-8424b90fdf8c.png)

연동후 위와 같은 페이지가 나타나지 않았다면 [ 여기로 ]( https://utteranc.es/) 들어가서 작업해주세요.

repo 하단 입력창에 권한을 부여한 레포지토리를 [user name]/[레포지토리명] 형식으로 입력하고, 

![image](https://user-images.githubusercontent.com/79133602/150095674-19d34aea-3133-4019-91f7-887052346b2f.png)

하단 Blog Post <-> Issue Mapping 메뉴에서 이슈에 작성된 내용중 해당 페이지에 관한 댓글만 표시하기 위한 방법을 원하는 대로 선택합니다.

![image](https://user-images.githubusercontent.com/79133602/150095757-d6afc28a-7f28-40ef-8d96-8dae41c16928.png)

Issue Label은 이슈가 생성될 때 다른 이슈와 구별하기 위해 해당 이슈에 라벨링을 할지 선택하는 옵션입니다. 
설정을 굳이 할 필요 없어서 skip했습니다. 

원하는 Theme이 있다면 선택하고

![image](https://user-images.githubusercontent.com/79133602/150096172-65df8bf0-8468-4f47-a787-5ec5e7cb126e.png)

위 속성값 선택으로 최종 완성된 스크립트를 복사해주세요.

![image](https://user-images.githubusercontent.com/79133602/150096288-c9186e3b-fde4-467a-8654-9f8e80fc25ef.png)

<br/><br/>
## 3. 사이트에 적용

```
<script src="https://utteranc.es/client.js"
        repo="bellasimi/bellasimi.github.io"
        issue-term="url"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
```

### ❗ jekyll minimal-mistakes 사용시

위 복사한 내용을 쓰지 않고, 위내용을 바탕으로 config.yml에 다음과 같이 입력해줍니다. 

![image](https://user-images.githubusercontent.com/79133602/150099265-52d62e51-8165-4265-b87f-052b45c101e8.png)


### ❗ 다른 테마 사용시

해당 스크립트를 posts.html의 댓글 div에 넣어줍니다. 


### ❗ 티스토리 등 블로그 스킨 사용시
 
티스토리 관리로 이동해서 스킨 편집을 클릭, html 편집을 누른 뒤 댓글 영역 태그인 <s_rp>를 검색해서 그 안의 기존 댓글 영역을 삭제하고
<div class="comment-form">안에 위 스크립트를 넣어줍니다. 
