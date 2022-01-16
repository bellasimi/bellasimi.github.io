---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- ajax
- axios
last_modified_at:
---

  
ajax는 서버에 새로고침 없이 요청이 가능하게 해주며 다음과 같은 방법으로 사용합니다. 

```
1. 제이쿼리 $.ajax()
  
2. axios설치 axios.get()
  
3. 자바스크립트 fetch()
```

그중에서도 우리느 2번째 방법 axios의 사용법을 알아보도록 하겠습니다.

<br/>

# 사용방법

먼저 다음 명령어를 터미널에 입력해 설치해줍니다.

```
yarn add axios
npm install add axios
```

설치가 완료되면 ajax 기능을 사용할 컴포넌트에서 import를 해주고

![image](https://user-images.githubusercontent.com/79133602/149661729-16221f3e-2278-4c1f-90ad-639f220ddef6.png)

axios 뒤에 다음 함수들을  붙여서 코드를 짜주시면 됩니다. 
 
| 함수 | 기능 |
|:---:|:----:|
| get() | 해당 링크값 가져오기 |
| then() | ajax 성공시 실행할 코드 |
| catch() | 실패시 실행 코드 |


![image](https://user-images.githubusercontent.com/79133602/149661733-edfddfa7-c08d-4ee8-a289-de7aeae61a77.png)

get함수에 넣어준 링크에 데이터를 잘 가져오면 then함수가 작동되고 성공이 콘솔창에 출력되지만 실패하면 catch함수가 작동되고 콘솔창에 실패가 출력됩니다. 


즉, 성공이라고 뜨던 위 코드 get의 링크를 아무렇게나 바꿔주면

![image](https://user-images.githubusercontent.com/79133602/149661901-70ce4585-9c5d-4996-9c5b-32a758320404.png)

아래처럼 콘솔창에 성공이라고 뜨던 기능이 실패를 띄웁니다.

![image](https://user-images.githubusercontent.com/79133602/149661973-21b541ab-1ec1-4f3d-a043-fbb891977504.png)
<br/><br/>

# 값 출력

.then()의 매개변수가 결과 자료가됩니다. ()안에 임의의 변수를 넣고 해당 변수명으로 자료에 접근이 가능한데요.

![image](https://user-images.githubusercontent.com/79133602/149661977-fc177562-69e8-4f2c-b946-4bb025aac818.png)

위 코드를 실행시키면 콘솔창에 다음과 같이 출력이 가능합니다.

![image](https://user-images.githubusercontent.com/79133602/149661976-67552c7d-ba39-4fc3-b541-1201848bd98f.png)

만약 데이터의 특정 인덱스, 속성값만 출력하고 싶다면 변수명[인덱스].속성 이런식으로 접근하면 되겠죠.


<br/><br/>
# fetch() 비교

사실 fetch는 위방법보다 잘 안씁니다. 호환성이 좋지 않기 때문인데요. 

![image](https://user-images.githubusercontent.com/79133602/149662205-a2aeed57-8c5a-42e9-9960-c9d18d82d51d.png)

fetch()에 데이터의 링크를 입력하고 받았을 때 브라우저에서 보면 object처럼 보이지만 사실 
json입니다. 잘보면 객체명 같이보이는 부분 ""에 쌓여있죠.

axios 쓰면 json 자료를 object로 알아서 바꿔주는 데 비해 fetch는 직접 해야되서 불편합니다.


<br/><br/>
# 활용 예시 : 상품 더보기 기능

더보기 버튼 누르면 get한 data를 화면에 표시하도록 해보겠습니다.

![image](https://user-images.githubusercontent.com/79133602/149662612-72faef69-383e-4af2-985a-0888873c6f16.png)

위와 같이 버튼에 onClick 값을 넣어주면 되는데요. 만약 라우팅된 컴포넌트라면, 해당 state와 setState 둘다 props로 보내주셔야 setState를 사용할 수 있습니다.

변경시에는 자료형이 같은 값을 넣어줘야 되서, 배열 스프레드 오퍼레이터로 복사 후 push()로 기존 state에 붙이고 그 값을 setState에 넣어주면 되는데요.

push 메소드 안쓰고 아래처럼 바로 spread operator로 배열 새로 만들 수도 있습니다.

```
setShoes([…shoes,…result.data]) 
```
<br/>
# ❗ ...spread operator 쓰는 이유

spread operator로 복사해서 넣어줘야 각행에 제대로 값이 들어갑니다. 

![image](https://user-images.githubusercontent.com/79133602/149662781-c1733354-578a-489c-9916-e4db285ee28e.png)

안그러면 1행에 3개의 데이터가 한꺼번에 들어가는점 주의하세요!

![image](https://user-images.githubusercontent.com/79133602/149662784-0ef60dcb-a30e-4c13-9c93-c77d113dce05.png)

<br/><br/>

# 더보기 버튼마다 다른 링크값 추가시

버튼 누른 회수를 저장하는 변수나 state cnt를 만들고 onClick에 콜백함수로 setCnt(cnt+1)를 넣어줍니다. 그리고
axios.get으로 받는 링크의 뒷부분 예를 들면 data2 이부분을 {"링크/data"+cnt변수+".json" } 이런식으로 바뀌도록해주면 클릭할 때마다 새로운 링크값을 순차적으로 get할 수 있습니다. 

<br/><br/>
# ajax 과정에 따른 ui 변화 : 로딩중 페이지

onClick 콜백함수에서 axios보다 먼저 로딩중 컴포넌트의 flag를 props.setLoading(true)로 바꾼뒤

![image](https://user-images.githubusercontent.com/79133602/149662956-da3d1544-aea5-44a8-a52e-c8cfba3aade0.png)

axios.get 이후 then과 catch에서 flag를 props.setLoading(false)로 바꿔 꺼주면 로딩중 페이지를 ajax 과정에 따라 조작할 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/149663034-1a8b562d-3239-4746-afd5-13f0fb8caaec.png)

<br/><br/>


#  axios.post : 서버에 데이터 보낼 때

헤더 설정 쿠키 저장등, 로그인시, 게시물 발행시 사용하는 기능인데요. 아래와 같이 코딩하시면 됩니다.

```
axios.post('서버url',{id:'내아이디',pw:1234});
```

<br/><br/>
# mount 하자마자 ajax 하고 싶을 떄

useEffect()를 사용하시면 됩니다. 만약 시작했을 때만 ajax.get()해오겠다하면 

![image](https://user-images.githubusercontent.com/79133602/149663198-f06e1fa0-9a68-49ee-a036-5307de5cf552.png)

이런식으로 짜고 get() 안에 링크값넣고, 성공시 then(), 실패시 catch()를 실행하도록 추가로 더 입력해주시면 됩니다. 