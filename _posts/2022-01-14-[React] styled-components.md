---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- styled-components
last_modified_at:
---
 
컴포넌트가 많아지면 일일이 css 만들기 복잡합니다. 실수로 className을 중복 사용하는 경우도 있죠 
그래서 styled-component를 사용합니다.

<br/>
# styled-component란?

Class 없이 css 스타일링 가능한 라이브러리로 class 선언 없이 컴포넌트에 Css를 직접 장착해 css in JavaScript라고 하기도 합니다.

장점은 class 중복을 방지한다는 건데 css 모듈화 해놓으면 class 중복될 일 거의 없어 취사선택하시길 바랍니다.

<br/>
<br/>
# 사용방법 

먼저 터미널에서 설치를 해줍니다.

```
yarn add styled-components

npm install styled-components

```

그리고  해당 컴포넌트 페이지에 라이브러리를 import를 한 뒤

```
import styled from 'styled-components';
```

컴포넌트 함수밖에 변수 만들어서 css 선언을 해줍니다. Css를 미리 입혀놓은 컴포넌트를 쓴다고 이해하시면 됩니다.

```
let 새박스 = styled.h4`
    font-size : 30px;
    padding : 20px;
    color : ${ props => props.색상 }
`;
```
<br/>
<br/>
# props 사용


만약 해당 태그에서 스타일 값을 받고 싶다면, props로 받아오면 되는데요.

![image](https://user-images.githubusercontent.com/79133602/149388775-9baf60f2-bdd8-4e8e-ac58-bcc58b124e18.png)


태그에 props명 = { 내용 } 또는 props명 = 내용 형식으로 전송할 style 값들을 입력후 (Component에 props 보낼 떄와 같음) 해당 styled-components에서 ${props => props.props명}으로 받아서 사용하시면 됩니다. 

<br/>
<br/>
# props 활용

> background : ${props => props.색상 || "yellow"}

태그에서 색상이라는 props값이 있다면 해당 값이 배경색이되고 색상이라는 props값을 받지 못했다면 노랑이 배경색이 됩니다.

![image](https://user-images.githubusercontent.com/79133602/149393074-ca4b0c86-f374-46f3-b0db-562e1806a191.png)


> {props => props.색상 && css`스타일`}

해당 props 존재시 && 뒤에 오는 css 스타일값으로 바꿔줍니다.

<br/>
## 사용법 

먼저 import styled,{ css } from 'styled-components'를 상단에 입력 후 다음과 같이 코드를 짜면

![image](https://user-images.githubusercontent.com/79133602/149395173-436647f3-191a-4bc3-bbea-4ae2625264bd.png)

변화라는 props값이 존재하면 글씨가 100px, 글씨색이 색상이라는 props값으로 변합니다.