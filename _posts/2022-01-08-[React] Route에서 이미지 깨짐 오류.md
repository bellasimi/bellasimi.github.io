---
title: 
sidevar:
  nav: "docs"
categories:
- react
- error
tags:
- react
- error
last_modified_at:
---

상세페이지를 라우팅하고, 해당 페이지에 보낸 props의 state 값을 이용해 img src를 지정하려고 했습니다.

![image](https://user-images.githubusercontent.com/79133602/148545187-48cf6cb1-c3cf-4a91-850d-e7fbdc454afd.png)

그런데 해당 작업을 완료하고 페이지를 띄워보니 이미지가 깨졌습니다. 😥

<br/><br/>
# 수정 전 상황


메인 App.js에 props를 제대로 보냈고

> App.js

```
<Route path="/detail/:id" >
    <Detail shoes = {shoes}/>
</Route>
```

props를 받는 Detail 컴포넌트에도 props가 제대로 전송이 됐습니다. 


> Detail.js

```
function Detail(props){
    return(
       <div className="col-md-6">
          <img src={"./img/"+props.shoes[id].img}  width="100%" />
       </div>
    )
}
```

화면에 해당값 [props.shoes[id].img}를 찍어보면 값이 잘 찍히는 것을 알수 있구요.

![image](https://user-images.githubusercontent.com/79133602/148545538-1cbc0ede-282e-4516-9935-fd04e10d3b91.png)

심지어 아래와 같이 직접 경로를 입력해도 이미지가 깨져서 나옵니다. 

```
<img src="./img/ipod.jpg"  width="100%" />
```

분명 App 컴포넌트에서는 정상 출력되는 경로인데, Detail 컴포넌트에선 왜 에러가 나는 걸까요? 🤔

<br/><br/>
# 에러 원인

일단 리액트에서 src 폴더에 이미지를 저장하고 쓰는 경우 다음과 같이 입력하셔야 합니다.
<br/>
## 컴포넌트에서 불러오기
```
import 이미지명 from ‘./이미지경로.jpg’
<img src={이미지명}>
```
 
## css에서 불러오기

```
background-image : url(‘이미지경로’)
```


App컴포넌트 역시 그렇게 해야 했는데 에러가 안난거고, Detail이 정상적으로 에러가 난 것입니다. 

그렇다면 일일이 사용할 img를 import 하고 또 img src를 따로 입력해야 하는데 너무 번거롭죠 😥 
그래서 아래 방법을 사용합니다.
<br/><br/>

# 해결 방법

require 모듈 키워드를 사용해 이미지를 불러옵니다. 

> Detail.js


```
<div className="col-md-6">
  <img src={require("./img/"+props.shoes[id].img)} width="100%" />
</div>

```
이제 잘 출력되는 것을 볼 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/148544761-7784f5ee-77bf-452c-8295-47c91bcd1a11.png)


만약 위코드가 먹히지 않는 다면 require() 뒤에 .default를 추가해주세요.

```
<div className="col-md-6">
  <img src={require("./img/"+props.shoes[id].img).default} width="100%" />
</div>

```
<br/><br/>


# 추가 설명

require는 nodeJS에서 사용되는 CommonJS 키워드로 import와 같은 역할을 합니다. import와 달리 상단에 입력값이 없어 
코드량이 적습니다. 다만, import의 경우 ES6 최근 모듈 시스템이기에 더 많이 사용됩니다. 

그리고 위의 상황은 제가 이미지 파일을 src 안에 넣어서 발생한 문제로 

만약 public/assets 폴더 안에 이미지를 넣어두셨다면, 다음과 같이 불러오시면 됩니다. 
<br/>
## 컴포넌트에서 불러오기

```
<img src = "/assets/이미지명.jpg">
```

## css에서 불러오기

```
<div style={ {backgroundImage:'url(/assets/이미지명.png)'} }>
```


<br/><br/><br/>

# 참고

💻 [public, src img 불러오는 차이] (https://velog.io/@rimo09/React-Create-react-app-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90%EC%84%9C-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EA%B2%BD%EB%A1%9C%EB%A5%BC-%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94-4%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95)

💻 [require VS import] (https://sowon-dev.github.io/2021/03/29/210330React-tip/)

💻 [require import 차이점] (https://hsp0418.tistory.com/147)

💻 [자바스크립트 CommonJS 모듈 내보내기, 불러오기] (https://www.daleseo.com/js-module-require/#:~:text=%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%20%EA%B0%9C%EB%B0%9C%EC%9D%84%20%ED%95%98%EB%8B%A4,%EC%83%88%EB%A1%AD%EA%B2%8C%20%EB%8F%84%EC%9E%85%EB%90%9C%20%ED%82%A4%EC%9B%8C%EB%93%9C%EC%9E%85%EB%8B%88%EB%8B%A4.)
