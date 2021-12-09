---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
last_modified_at:
---

> React 프로젝트 생성 및 node.js 서버에 연결 

리엑트를 사용하기 위해선 node.js를 설치해야 합니다. 만약 없으신 분은 [이 페이지](https://bellasimi.github.io/%EC%A0%9C%EC%9D%B4%EC%BF%BC%EB%A6%AC-%EC%9D%B8%EC%8B%9D-%EC%98%A4%EB%A5%98/#%ED%95%B4%EA%B2%B0-%EB%B0%A9%EC%95%88)
를 보고 다운로드 받아주세요
😉

<br/><br/>


# 1. React 프로젝트 생성

원하는 디렉토리 위치 터미널에서 npx create-react-app 프로젝트명 입력해 줍니다. 

저는 node.js로 서버를 돌리고 React는 view를 작업할 때만 쓸 예정이라 node프로젝트 하위 폴더에 React프로젝트를 만들어 줬습니다. 

<br/>
❗ npm 툴 node js 개발환경 안에 create-react-app 라이브러리가 있기 때문에 node.js가 제대로 설치되지 않았다면 오류가 나니 설치가 제대로 됐는지 확인해 주세요 ❗

<br/><br/>


# 2. React 작동 확인

해당 위치(React 프로젝트가 존재하는 디렉토리)에서 터미널에 npm start를 입력하면 
port 3000으로 react 프로젝트의 index.html을 띄워볼 수 있습니다.

![image](https://user-images.githubusercontent.com/79133602/144593245-fac9e4ca-b966-465d-8d21-045edc668c28.png)

기본값으로 App.js에 입력된 값이 잘 출력되는데요. 

이 화면을 바꿔 주기 위해선 App.js의 내용을 바꿔주면 됩니다. 

전 다음과 같이 바꿔줬습니다. 

```
    <div className="App">
         <img src={logo} className="App-logo" alt="logo" />
            <div className="Resume">
                <p>
                안녕하세요 BackEnd 개발자 Shin입니다.
                </p>
            </div>
    </div>  
```

이제 port:3000으로 접속시 화면이 제가 입력한 값으로 바뀐 것을 볼 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/144580342-f9e90de6-0249-4b99-a05d-920b69c18a73.png)

그런데 node 서버에선 위 화면이 나오지 않습니다. 아직 아무런 설정을 해주지 않았기 때문입니다.

<br/>
<br/>


# 3. node 서버에 React로 만든 페이지 연결 

node서버에 index.html을 띄우기 위해선 상위 디렉토리 node.js 프로젝트의 app.js를 수정해야합니다. 

node 서버에서 "/profile"이라는 매핑주소를 입력시 react프로젝트의 index.html이 뜨도록 할 예정인데요.

그러려면, 먼저 react 프로젝트 위치에서 터미널에 npm run build를 입력해 배포가 가능한 상태로 만들어 줘야합니다.


그다음 node 프로젝트의 app.js에 다음 코드를 추가합니다. 


```
app.use(express.static(path.join(__dirname,"profile/build")));

app.get("/profile",(req,res) => {
    res.sendFile(path.join(__dirname,"profile/build/index.html"));
});

```

그러면 이제 node 서버에서도 "/profile"이란 매핑주소로 React로 만든 페이지를 띄워볼 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/144595101-bd99d975-4864-428d-9fd2-6289ba4d37de.png)

<br/>
<br/>

# React 작동원리 


React 프로젝트의 파일목록을 봅시다.

![image](https://user-images.githubusercontent.com/79133602/144595633-56956003-6bfb-40ef-911a-db0e74e0da8b.png)

* build :  npm run build 명령어 이후 생성되는 폴더, 배포에 필요

* node_modules:  라이브러리 모은 폴더

* public : static 파일 보관함 폴더 build해도 압축 안된 상태로 남아 있음

* src : 소스코드 보관 폴더

* public/index.html : 화면에 나타나는 파일

* src/App.js : 화면에 무엇이 보일지 입력한 파일

* src/index.js : 어떤 컴포넌트를 어떤 view에 렌더링해줄지 입력한 파일

* package.json 설치한 라이브러리 목록이 입력된 파일- > 버전 변경 가능 


이중 index.html, index.js, App.js를 보면 어떤식을 view를 조작하는 지 알 수 있습니다. 

먼저 화면에 나오는 index.html 파일의 root라는 id의 div를 보면 빈칸입니다. 

![image](https://user-images.githubusercontent.com/79133602/144577799-2cbd69d1-9913-43b3-8245-47cefa0e0e9e.png)

즉 해당 html에서 값을 직접 입력하는 게 아니라, 다른 파일에 입력한 컴포넌트를 root라는 div에 불러와 쓰는 방식인데요.

여기에 값을 보내려면 어떻게 하는 걸까요?

바로 값을 보내기 위해  ReactDOM.render() 메소드를 사용해 <App/> 컴포넌트가 root라는 id를 가진 요소에 렌더링작업을 해야 합니다. 

이 일을 src/index.js가 하고 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/144578165-587bf0ef-ab53-47c6-9abf-8b849505d696.png)


<App /> 컴포넌트는  src/App.js  <div className="App"> 안의 내용을 의미합니다. 


src/App.js에 다음과 같은 내용을  입력 후  App 컴포넌트를 내보내면  

```
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
         <img src={logo} className="App-logo" alt="logo" />
            <div className="Resume">
                화면에 보여질 내용
            </div>
    </div>  
  );
}

export default App;

```

index.js가 받아서 렌더링 해줍니다. 

<br/>
<br/>
<br/>

# 참고 


💻 <https://velopert.com/reactjs-tutorials>

💻 <https://ko.reactjs.org/docs/getting-started.html>






 
