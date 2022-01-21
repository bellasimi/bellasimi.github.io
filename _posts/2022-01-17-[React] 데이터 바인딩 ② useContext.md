---
title: 
sidebar:
  nav: "sidebar-list"
categories:
- react
tags:
- react
- useContext
last_modified_at:
---

App 컴포넌트에서 생성한 state를 다른 컴포넌트에서 쓰려고 할 떄 전엔 props를 통해 전달해줬습니다. 간단한 데이터를 내보내기엔 편하지만 관리가 필요한 복잡한 데이터, 또는 여러번 props해줘야 되는 데이터의 경우엔 props를 여러번 사용하는 게 불편합니다. 이럴 때 props 대신 useContext() 또는 redux를 사용해 값을 전송하면 편한데요. 오늘은 그 중에서 useContext()에 대해서 알아보도록 하겠습니다.

<br/>
# useContext() 

useContext는 react라이브러리의 훅으로 Context명.Provider 태그의 value값을 받아 변수에 저장할 수 있게해주는데요. 예를 들어 App 컴포넌트에서
상품별 재고량을 left라는 state로 만들고  App 컴포넌트 아래 > Main > Device 컴포넌트에 전송하려면 props를 두번쓰는 대신 다음과 같이 하시면 됩니다. 


<br/>
<br/>
# 사용법 

<br/>
## 1. 전송하기 : App 컴포넌트

App 컴포넌트 밖에서 React.createContext()로 state를 담아줄 공간을 생성해줍니다.

![image](https://user-images.githubusercontent.com/79133602/149766335-7284a482-9e9a-4428-824d-d0cf429f4866.png)

전 leftCon이라는 이름으로 공간을 생성해줬습니다. 그리고 App 컴포넌트에서 left라는 state를 leftCon.Provider 태그의 value로 넣어줍니다. 

![image](https://user-images.githubusercontent.com/79133602/149766579-099d24f0-fbf4-40f8-87e9-e5e735f98b13.png)

redux에서 Provider 태그를 쓰기위해 react-redux에서 Provider를 import했던 것과 달리 여기선 import없이 그냥 바로 
전송해줄 컴포넌트를 아래와 같이 감싸주면 됩니다. 

![image](https://user-images.githubusercontent.com/79133602/149767265-54c80a09-c1d9-4a2f-a2b3-41595704cd49.png)

<br/>
## 2. 전송받기 : Device 컴포넌트

먼저 해당 컴포넌트 파일 상단에 useContext를 import를 해줍니다. 그리고 컴포넌트의 변수에 useContext(leftCon)으로 state를 받아 새로운 state를 만들어줍니다.

![image](https://user-images.githubusercontent.com/79133602/149767966-f9ff8506-8754-4280-a8cd-880180bd9037.png)

그러면 App>Main>Device 순서로 컴포넌트가 이뤄져있어도 App에서 보낸 값을 바로 하하위 컴포넌트인 Device에서 쓸 수 있습니다. 


<br/>
<br/>
# 모듈화한 경우 

만약 하위 컴포넌트를 분리해서 다른 파일로 만든경우 각각 React.createContext()로 만든 공간을 export, import해줘야 합니다. 예를 들어 Detail이라는 모듈화된 컴포넌트에 App 컴포넌트 데이터를 useContext()로 전송한다면 

App.js 에서 다음과 같이 leftCon을 export 하고 (leftCon변수 아래에서 코딩해야 인식!) 

```
export { leftCon };
```

Detail.js에서 imoprt를 하면 

```
import { leftCon } from './App,js';
```

나머지 과정은 아까와 같습니다. 

App에서 <Detail/> 컴포넌트를 <leftCon.Provider value = { left }>로 감싸주고, Detail에서 useContext(leftCon)으로 state를 받아 사용하시면 됩니다!
