---
title: nodeWeb
sidevar:
  nav: "docs"
categories:
- js
tags:
- js
- node
- project
last_modified_at:
---
오늘은 node.js를 사용해 웹페이지를 구현하는 방법에 대해 알아보도록 하겠습니다. 😉

<br/>

# 1. 기본 설치

일단 cmd 창을 열어서 node -v를 입력해 주세요 

![image](https://user-images.githubusercontent.com/79133602/144048962-579af8c8-0bb8-4cf6-8a2d-8d276e0b6f8f.png)

제대로 설치가 됐다면 저처럼 버전이 나와야 하는데 없으면 나오지 않습니다. 

그럴때는 
[node.js 설치](https://bellasimi.github.io/%EC%A0%9C%EC%9D%B4%EC%BF%BC%EB%A6%AC-%EC%9D%B8%EC%8B%9D-%EC%98%A4%EB%A5%98/#%ED%95%B4%EA%B2%B0-%EB%B0%A9%EC%95%88)
를 해주세요


node.js 설치후

cmd 창에서 cd 명령어로 원하는 위치로 이동 또는 mkdir 디렉토리명입력 후 해당 위치에서
다음 명령어를 입력해 기본 파일을 설치해 줍니다. 

```
npm init -y
npm install express
```


설치가 다 됐다면 개발 툴로 만든 디렉토리를 열어줍니다. 

<br/>
<br/>

# 2. 웹 설정

![image](https://user-images.githubusercontent.com/79133602/144050061-df515fcc-84b6-441e-861a-c0a349ecfa37.png)

디렉토리를 열면 위에서 views폴더 app.js제외하고 저와 같을 겁니다. package.json을 제외하곤 건드리지 말아주세요!

저와 같은 위치에 app.js를 만들고 그안에 다음과 같이 코드를 짜줍니다.



```
/* express불러오기 */
const express = require("express");

/*웹서버 생성*/
const app = express();

app.get("/",(req,res) => {
    res.send("HOME");
});
app.listen(5050,() => console.log("server : http://localhost:5050"));
```



이후 node app.js를 개발툴 터미널에 입력하면 port5050 서버가 실행되면서 

툴 터미널엔 hello world!가 웹페이지엔 HOME이라는 글이 뜹니다. 

하지만, 서버를 작동한 후 수정사항이 있을 때마다 서버를 재시작해야 되서 불편한데요.

nodemon이라는 확장 모듈을 설치하면 파일 수정시 자동으로 노드 어플리케이션을 재시작할 수 있으니 다운로드 받아 주세요.



```
npm install -D nodemon 
```


명령어에 -D 추가하면 개발자가쓰는걸로 인식을 하고 package.json에 들어갑니다. 

터미널에 node app.js 대신  nodemon app.js를 입력하면 되는데 단축키를 쓰고 싶으시다면 package.json scripts에 



```
  "scripts": {
    "단축키 이름": "nodemon app.js"
  },

```


이런식으로 수정 후 터미널에 npm 단축키 이름을 입력하시면 됩니다. 

<br/>
<br/>


# 3. 서버에 페이지 띄우기


app.js 페이지 내 app.send()의 변수로 html 값을 넣어주는 방법이 있지만 너무 지저분하죠.

이때 pug라는 템플릿 엔진을 쓰면 app.render("pug파일명")라는 코드로 간단히 페이지를 구현할 수 있습니다.


그러기 위해서 설치를 해주고 

```
npm install pug //(== npm i pug)
```

app.js에서 아래 코드를 추가로 입력해 pug를 view engine으로 등록을 시켜줍니다. 

```
//views라는 디렉토리에서 pug파일들을 관리
app.set("views",__dirname+"/views");

//view engine으로 등록
app.set("view engine","pug");

```

그 다음 views라는 폴더에 index.pug 파일을 만들고 아래처럼 코드를 입력해주세요.


```
doctype html
html(lang="en")
  head
    meta(charset="UTF-8")
    title= About pug
    script(type='text/javascript').
    	console.log("pug에 대해 설명")
	style #container {color: red;}
  body
    h1 HOME
    p 이것이 바로 pug로 작성한 페이지입니다!

    #container.col
      if condition
        p true
      else
        p false!
```
pug의 형식으로 작성된 코드를 html형식으로 변환해 보면 다음과 같습니다. 


```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>About pug</title>
    <script type="text/javascript">
     	console.log("pug에 대해 설명")
    </script>
  </head>
  <body>
    <h1>HOME</h1>
    <p>이것이 바로 pug로 작성한 페이지입니다!</p>
    <div id="container" class="col">
      <p> false!</p>
      </div>
  </body>
</html>
```

그리고 app.js에  아래 코드를 추가해 주면 해당 index.pug 파일을 "/" 매핑주소로 서버에 등록시켜줄 수 있습니다. 


```
app.get("/",(req,res) => {
    res.render("index");
});
```
 
<br/>
이제 아래와 같이 port 5050에 입력한 값으로 웹페이지가 뜨면 성공입니다! 😎

![image](https://user-images.githubusercontent.com/79133602/144048313-097f6450-0cb4-4ee3-952e-4d7e4554a7eb.png)

<br/>
<br/>
<br/>

# 참조 

💻 [pug로 html 템플릿 만들기](http://haneul-lee.com/2021/05/pug%EB%A1%9C-html-%ED%85%9C%ED%94%8C%EB%A6%BF-%EB%A7%8C%EB%93%A4%EA%B8%B0/)
