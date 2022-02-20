---
title: 
categories:
- react
tags:
- react
- redux
- reducer
- dispatch
last_modified_at:
---


redux는 index.js에서 Provider태그를 가지고 상위 컴포넌트 App에 state를 전송하고 reducer를 통해 데이터를 관리하기 떄문에 여러 컴포넌트에서 반복적으로 나타나는 데이터를 전송할 때 사용하면 편리합니다.

<br/>
# 사용법

먼저 터미널에서 react-redux와 redux를 설치를 해줍니다.

```
npm install redux react-redux
yarn add redux react-redux
```
<br/>
## 1. index.js setting

index.js 파일에 가서 상단에 다음과 같이 import를 해준 다음 createStore()를 사용해 변수를 만들어줍니다.

![image](https://user-images.githubusercontent.com/79133602/149955133-a386d822-4b83-4a7b-ada0-b07d6ebff07c.png)

그리고 데이터를 전송할 App 컴포넌트 주위를 Provider 태그로 싸고 store 속성값으로 createStore()로 만들어 놓은 변수를 입력합니다. 이러면 이제 모든 컴포넌트에서 다음과 같은 방식으로 값을 받을 수 있습니다. 
<br/>
## 2. useSelector() 

값을 전송받는 컴포넌트 파일로 가서 상단에 다음과 같이 import해줍니다.

```
import { useSelector } from 'react-redux';
```

그리고 컴포넌트에 변수선언을 한 뒤 

```
let 변수명 = useSelector((state)=>{return state})
또는 = useSelector((state)=> state)
```

useSelector의 콜백함수로 state를 return하고 그 값으로 초기화를 시켜줍니다. 컴포넌트에선 이제 props붙일 필요없이 그냥 변수명으로 사용하시면 되는데요. 만약 객체의 특정 속성값만 가져오고 싶다면 state.속성명으로 return하시면 됩니다. 

<br/>
## 2-1. connect : state props로 변환

react-redux 라이브러리에서 connect를 import하고

```
import { connect } from 'react-redux';
```

컴포넌트 밖 페이지 하단에 state를 props로 변환해줄 함수를 만들어 줍니다. 

```
function makeProps(state) {
  return{
    state : state; 
  }
}

```

그리고 그 함수를 connect()로 해당 컴포넌트와 함께 export해줍니다. 

```
export default connect(makeProps)(Detail)
```

그러면 이제 Detail 컴포넌트의 props로 state에 접근이 가능합니다. 단, 이방식은 useSelector() 보다 코딩량도 많고 번거롭습니다. 

<br/>
## 3. reducer : store 관리

만약 컴포넌트에서 조건에 따라 redux store값을 바꾸고 싶을 땐 어떻게 해야 할까요?

![image](https://user-images.githubusercontent.com/79133602/149959446-d7c298f4-368c-4e92-8de0-2d64db13a08c.png)

예를 들어 장바구니에서 +를 누르면 상품의 수량이 1씩 증가하고 -를 누르면 수량이 1씩 감소하도록 해보겠습니다. 

일단, index.js로 가서 다음과 같이 컴포넌트 밖 상단에 reducer 함수를 작성해줍니다. (함수명이 reducer일 필요는 없습니다.)

![image](https://user-images.githubusercontent.com/79133602/149959359-fa559faa-7231-43ba-9268-11e102795f41.png)

여기서 reducer의 첫번째 매개변수 state=기본값은 기본값이라는 변수가 state의 default값이라는 뜻이고, 두번쨰 매개변수 디스패치는 컴포넌트에서 props.dispatch()또는 useDispatch로 보낸 값을 의미합니다. 

그리고 reducer 함수 안에서 state가 변형되지 않도록 spread operator를 써서 복사본을 만든 후 조건에 따라 조작해서 return하도록 합니다. 

만약 state를 return하지 않으면 error가 나니 확인해주세요!

<br/>
## 4. useDispatch() : reducer에 조건 전송

이제 장바구니 컴포넌트로 돌아가서 상단 react-redux라이브러리에 useDispatch를 import해줍니다. 

```
import { useSelector,useDispatch } from 'react-redux';
```

그다음 컴포넌트 함수에 다음과 같이 변수 선언을 하고 useDispatch()로 초기화를 한뒤 

```
let dispatch = useDispatch();
```

dispatch의 매개변수로 객체 데이터에 type,idx 속성값을 넣어 넘기시면됩니다.

![image](https://user-images.githubusercontent.com/79133602/149961743-746c3d42-c05a-4c86-a1ce-7b0a029d3a37.png)

그럼 그 값을 reducer가 디스패치로 받아 조건문에 디스패치.속성명으로 사용할 수 있습니다. 

<br/>
## payload로 값 전달


이제 버튼에 paylaod, 또는 data 속성으로 데이터 값을 보내 그 값만큼 증가 시켜보도록하겠습니다.

![image](https://user-images.githubusercontent.com/79133602/154848765-0abdbdb6-99b1-4f21-bfe4-c17e454e83ec.png)


Reducer()의 두번째 매개변수가 dispatch의 값이므로, 객체의 payload값에 접근하기 위해 디스패치.payload라고 쓴뒤 type==="+" 일 떄 조건문을 다음과 같이 수정합니다.

![image](https://user-images.githubusercontent.com/79133602/154848770-e8a90bde-b784-4474-a59b-9245b9b70d87.png)


그럼 이제 1이 아니라 payload로 보낸 값만큼 증가하는 것을 볼 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/154848774-7ed30b36-a253-4b98-970e-1f964a780e70.png)

<br/>
# 예시 2 : 장바구니에 값 추가

Detail 컴포넌트의 장바구니 버튼을 누르면 해당 상품의 데이터를 장바구니 데이터에 추가해봅시다.


<br/>
## 0. redux 사용전 setting
 
먼저 해당 컴포넌트에서 redux를 사용하려면 redux의 state를 props로 바꿔주는 함수와 
Connect 기능이 필요합니다. 

```
Import { connect } from 'react-redux';


Function detailRedux(state) {
     return {
	State : state.reducer
     }
}
Export default connect(detailRedux)(Detail)

```

<br/>
## 1. props.dispatch()

장바구니 버튼을 누르면  아래 정보들을 dispatch로 reducer에 전송합니다.

![image](https://user-images.githubusercontent.com/79133602/154848786-2ce1c33e-585e-4fdb-a367-de01d8a3d36b.png)


> props.dispatch( { type: "addGoods", payload: 해당 신발의 데이터 })

그런데 개발환경에서 새로 고침하면 redux도 초기화됩니다. 그러니 이를 방지하고 싶다면, 새로고침없이 바로 페이지 이동이 가능하도록 onClick 콜백함수 내에 history.push("/cart")를 써줍니다. 


<br/>
## 2. reducer 조건문 

그리고 Index.js의 reducer에서 디스패치.type === "addGoods" 조건일 떄 state 배열에 디스패치.payload 값을 push하도록 합니다. 

![image](https://user-images.githubusercontent.com/79133602/154848794-0e1d75fe-e353-4392-960c-90621f80109f.png)


만약 같은 상품을 담았다면, 새로운 행에 추가되는 대신 해당 상품의 수량만 증가시켜줘야합니다. 

그래서 아래와 같이 조건을 추가 합니다. 

![image](https://user-images.githubusercontent.com/79133602/154848801-4e4704f5-7736-4a06-aab1-7939e3b73f88.png)

<br/>
여기서 주의점은 idExist 변수 선언이 해당 addGoods조건일 때 이뤄져야 한다는 겁니다.
만약 다른 type조건일 떄 또는 전역에서 선언되면 디스패치.payload.id라는 값이 존재하지 않아 에러가 납니다.!

## props.dispatch() : 옛날 방식

옛날에는 useDispatch()대신 props로 dispatch값을 보냈습니다. 이경우에 import할 라이브러리는 없습니다. 
그냥 props.dispatch(데이터) 이런식으로 넘기면 끝입니다. 

<br/><br/>
# 너무 복잡한거 아냐?

소규모 프로젝트시엔 필요 없을 수도 있습니다. 하지만 state가 100만개 넘어가는 대형사이트들은 redux 안쓰면 데이터 관리가 어렵습니다.
state가 이상해졌을 때 redux 안썼다면 props를 일일이 뒤져봐야 하는데 불가능하죠.

반면 redux는 state이상해졌을 때 props.dispatch()랑 reducer()만 찾아보면 되서 이럴 때 필요합니다.



<br/><br/>
# reducer가 여러개일 때

만약 새로운 reducer를 만들 때 어떻게 store에 모든 reducer state들을 담을 수 있을까요?

![image](https://user-images.githubusercontent.com/79133602/149963737-eb296e1e-7ade-4975-a231-79c9f30f4203.png)

위와같은 새로운 reducer가 있을 떄 기존 reducer와 함께 state를 전송하고 싶다면 combineReducer를 사용하면 됩니다.

그러기 위해서 index.js에서 combineReducers를 아래와 같이 import해주고

![image](https://user-images.githubusercontent.com/79133602/149963279-85089ce6-535d-4884-b26c-c5b39367d14e.png)

그 아래 combineReducers({})를 사용해서 createStore()에 여러 state의 
Reducer를 담아줍니다.


![image](https://user-images.githubusercontent.com/79133602/149964179-6542208e-2149-406b-8c32-b76deb3a5825.png)

이제 장바구니에서 state를 받으면 state.reducer, state.reducer2로 각각의 값에 접근할 수 있습니다. 각각의 값에.속성을 붙이면 속성값에 접근 가능하구요.

<br/><br/>

# 주의점

자, 여기까지 여러개의 state 값을 redux로 어떻게 전송할지 알 기 쉽게 쓴 예시였는데요. 이건 이해를 돕기 위한 단순값이고, 이런 단순값은 redux를 쓰지 않습니다. 

redux store는 온갖 데이터 저장하는데 쓰지 않습니다. 대량의 정보 전달 및 관리에 용이하기 때문에 이렇게 특정 구역에서 flag의 값을 저장할 땐 redux대신 해당 페이지에서useState()를 쓰고 복잡한 데이터를 전송관리시에만 쓰도록 합니다.





