---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- routing
- react-router-dom
last_modified_at:
---

리액트는 알시다시피 하나의 페이지만을 사용하죠. 그런데 여러페이지를 띄우고 싶다면 어떻게 해야 할까요?

<br/>
# 라우팅

리액트에서 페이지를 여러 개 띄우기 위해선 react-router-dom 라이브러리 사용해 라우팅을 해줘야 합니다.(페이지 나누기)

```
Yarn add react-router-dom@5

Npm install react-router-dom@5
```

터미널에 위 명령어 중 하나를 입력하면 설치가 완료되는데 이후에 다음과 같이 초기 설정을 해줘야 합니다.

<br/><br/>
# 1. 초기 SETTING

Index.js 에 BrowserRouter 또는 HashRouter를 import하고 reder 함수안에  해당 태그를 넣어줍니다.

```
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
        <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
);

```

둘의 차이점은 아래와 같으니 원하는 태그를 넣어주시면 됩니다. 


> HashRouter 

HashRouter는 라우팅을  안전하게 할 수 있게 해줍니다. 
사이트 주소 뒤에 #이 붙는데 # 뒤에 적은
것은 서버로 전달되지 않고 리액트에서 처리하기 때문입니다.

> BrowserRouter

반면, BrowserRouter는 사이트 주소 뒤에 바로 경로가 오는데 이게 
리액트가 아닌 서버로 전송될 수 있습니다. 이런  경우 존재하지 않는 페이지를 
서버에 요청하는 꼴이 나서 에러가 납니다. 


<br/><br/>
# 2. path 지정

App.js 파일 상단에 아래와같이 라이브러리를 import해주세요.

```
import {Link, Route, Switch } from 'react-router-dom';
```

그리고 App 컴포넌트 안에 Route태그를 사용해 path를 지정해주면, 해당 path로 접속시, 해당 태그 안의 html 내용만 나오는 것을 확인할 수 있습니다.

예로, 
```
<Route path="/">
  <div>메인페이지</div>
</Route>
<Route path="/detail">
    <div>디테일</div>
</Route>
<Route path="/abc" component={Modal}></Route>
function Modal(){

    return(
        <div>
            <p>ABC페이지</p>
        </div>
    );

}

```
App 컴포넌트 안에 이렇게 코딩을 하면 각각 다음과 같이 화면에 나타나는 것을 볼 수 있습니다.

> http://localhost:3000/

![image](https://user-images.githubusercontent.com/79133602/148067274-7b483cbd-dc0e-41af-a063-b45637d1bdef.png)


> http://localhost:3000/detail

![image](https://user-images.githubusercontent.com/79133602/148067282-0f65349e-14b6-4de0-9659-a3328ecce01e.png)


> http://localhost:3000/abc

![image](https://user-images.githubusercontent.com/79133602/148067292-132a3dc0-8ebc-49f6-b6f5-bb208b462770.png)


지금 "/" 경로는 /로시작하는 모든 경로값을 포함하기에 
다른 경로 페이지에서도 메인 페이지라는 값이 계속 출력되는데
이걸 "/" 경로일 때만 나타나도록 하고 싶다면 

> Route exact path="/"

Route 태그 path 앞에 exact만 추가해주시면 됩니다. 



  