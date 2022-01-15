---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- useEffect
last_modified_at:
---



컴포넌트엔 인생주기 lifecycle가 있습니다. 
마운트, 언마운트시 (등장 업데이트), 재렌더링되고 퇴장하는 모든 순간인데요. 
이 각각의 순간마다 훅을 걸면 특정 순간에 작동되는 명령을 만들 수 있습니다. 

<br/>
# Lifecycle Hook 

원래 class 컴포넌트로 다음과같이 만들었는데요

```
Class Detail2 extends React.COMPONENT {
  componentDidMount(){
	  //Detail2 컴포넌트 Mount 쵔을 때 시랭할 코드 등장
    Ajax 같은 것도 사용 
  }
  
  componentWillUnmount(){
    //Detail2 컴포넌트 사라질 때 전에 실행할 코드
  }
```

 이젠 useEffect()라는 함수를 사용합니다.
<br/>
#  useEffect 

먼저 해당 컴포넌트 페이지에서 useEffect를 import해주고

![image](https://user-images.githubusercontent.com/79133602/149624968-ea40b9e5-e8b8-425f-9204-93dc5babe6c1.png)

2초가 지내면 경고창이 사라지도록 코드를 짜보겠습니다.

![image](https://user-images.githubusercontent.com/79133602/149625014-cd107851-a8af-46ef-9077-f1702ef2a384.png)

alert라는 state에 경고창의 switch값 true를 넣습니다.

그리고 useEffect 함수 안에 콜백함수 만들고 안에, setTimeout()메소드를 이용해 2초가 지나면 스위치를 false로 바꿔 경고창이 사라지게 합니다.

![image](https://user-images.githubusercontent.com/79133602/149625009-0a87b01c-77bb-469f-b3e1-d91df72076df.png)

그냥 setTimeout()을 바로써도 되지만 가독성과 관리가 용이하도록 변수로 만들어 호출하도록 합니다. 


useEffect()를 여러개 만들 수 있는데 그런 경우 순서대로 실행됩니다.


<br/><br/>
# 문제점

컴포넌트 등장 업데이트 둘다 실행되기에 버그가 발생할 수 있습니다.

![image](https://user-images.githubusercontent.com/79133602/149625299-b8c0caa1-eb72-4041-a955-a7647687ba63.png)

예로 위와같은 경우  컴포넌트 input값이 업데이트가 될때마다 useEffect() 계속 실행됩니다. 그리고 재렌더링이 되서 자원낭비가 심합니다.

맨처음 로드될 떄만 실행되게 하고 싶은데 그럼 어떻게 해야 할까요?

<br/><br/>
# 해결법

특정 state가 변경 될때만 실행하도록 조건을 부여해주면 됩니다.

![image](https://user-images.githubusercontent.com/79133602/149625377-ba351377-1979-45d1-ad3b-c9ed40c604fd.png)

위는 alert라는 state가 변경될 때만 실행해달라는 뜻입니다.

[안에 state명 여러 개 넣기 가능, 이런식으로] 가능하고, []로 아무 조건이 없으면, 페이지 로드 됐을 때 한번 실행하고 끝납니다.

<br/><br/>
# setTimeout() 문제

시간 초과전 뒤로가기 눌렀을 때라던가 쌓이면 오류가 납니다. 그래서 return 값으로 clearTimeout(타이머)를 줘서 타이머 해제를 해줘야 합니다.

![image](https://user-images.githubusercontent.com/79133602/149625540-be38de29-f63d-4c23-be34-a5288381b57f.png)

