---
title: 
sidevar:
  nav: "docs"
categories:
- error
tags:
- react
last_modified_at:
---

> npx create-react-app 프로젝트명

평소처럼 리엑트 프로젝트를 만드려고 코드를 입력했는데 다음과 같은 에러를 만났습니다. 

![image](https://user-images.githubusercontent.com/79133602/146645370-83818286-c1e1-4555-beae-5d25c0235d32.png)

# 원인

컴퓨터에 이미 create-react-app이 깔려있는데 더이상 지원하지 않는 버전이라 나온 문구입니다. 😥

# 해결방법

먼저 아래 코드로 creact-react-app을 삭제해줍니다.

> npm uninstall -g create-react-app

그다음 create-react-app을 재설치해주는데, 만약 npm 버전이 5.1보다 구버전이라면

> npm install -g create-react-app
> create-react-app 프로젝트명

이라고 입력하시고, 이보다 최신 버전이라면

> npm add create-react-app
> npx create-react-app

이라고 입력하시면 됩니다. 



## 💥 npm 버전 확인

터미널에 npm -v 라고 치면 현재 깔린 버전이 나옵니다. 
