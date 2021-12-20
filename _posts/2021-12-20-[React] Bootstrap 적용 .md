---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- bootstrap
last_modified_at:
---

프론트엔드 작업을 할 때 직접 css를 하기 귀찮다면, css 라이브러리 bootstrap을 이용하면 됩니다. 
리액트에도 마찬가지로 적용가능한데요. 다음과 같은 방법으로 사용하시면 됩니다. 

<br/><br/>

# Bootstrap 설치

## 1. CDN 설치

해당 프로젝트의 public 폴더 - index.html의 <head> 태그 밑 <link> 태그들을 모아 두는 자리에 
  
```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3"crossorigin="anonymous"/>

```

위 코드를 입력해 줍니다. 
  
  
그러면 부트스트랩이 호스팅해주는 파일을 받아 css로 적용할 수 있습니다. 
  
단 서버가 불안정할 경우 문제가 생길 수 있습니다. 
  
<br/>

## 2. yarn, npm 내부 설치

프로젝트 터미널에 
  
```
npm install react-bootstrap bootstrap@5.1.3
```
또는 아래와 같이 입력해줍니다. @5.1.3은 제가 지정한 버전이므로 빼도 무방합니다. 
  
```
yarn add react-bootstrap bootstrap@5.1.3
```
  

<br/><br/>
  
# 적용방법
  
[부트스트랩](https://getbootstrap.com/docs/5.1/getting-started/introduction/)에 접속, 
Docs 메뉴에서 원하는 UI를 검색해서 리액트 프로젝트에 
붙여넣기 해줍니다. 

전  부트스트랩에서 제공하는 빨간 버튼을 써보도록하겠습니다.


```
<button type="button"class="btn btn-danger">부트스트랩적용</button>
```
  
  
App 컴포넌트의 return문에 위 코드를 입력하고 서버에 페이지를 띄워보면

![image](https://user-images.githubusercontent.com/79133602/146743730-683789ff-4ff9-4478-89f6-ed6ab30260c3.png)  

부트스트랩 CSS가 잘 적용되는 것을 볼 수 있습니다. 
  

# 실패했다면?
  
CSS가 적용되지 않아 아래처럼 평범한 button이 생성됩니다. 
  
![image](https://user-images.githubusercontent.com/79133602/146744074-dd6893b9-6aaf-4984-afed-3d9e72f218f3.png)
  
 public - index.html의 link가 잘 입력됐는지 확인하고, npm yarn으로 내부 설치가 제대로 됐는지 확인해주세요!

<br/>
<br/>

# 참고

💻 [부트스트랩](https://getbootstrap.com/docs/5.1/getting-started/introduction/)

💻 [리액트 부트스트랩](https://react-bootstrap.github.io/)
