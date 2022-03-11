---
title: 
categories:
- react
tags:
- react
- useRef
last_modified_at:
---

<br/>
자바스크립트에서 DOM을 조작할 땐 queryselector나 getElementById, getElementByClassName DOM Selector메소드를 사용했죠. 하지만 리액트에서 그런식으로 DOM을 조작하면 안 됩니다. 대신 useRef() 훅을 사용해야 합니다. 

# useRef란

.current 프로퍼티에 변경가능한 값을 담고 있는 상자와 같습니다. 그리고 다음과 같은 특징을 갖고 있습니다. 

## 1. 값을 유지
useRef는 순수 자바스크립트 객체를 생성하고, component가 mount될 때 react-dom코드 내부 전역변수에 초기값을 저장합니다.
update가 되도 계속 이 값을 가져오기에 가변값을 유지하는 데 편리합니다. 


## 2. 컴포넌트의 리랜더링이 없다

이벤트 객체와 달리 useRef는 .current 프로퍼티가 변했다고 해서 컴포넌트가 리렌더링 되지 않습니다. 
그러므로 불필요한 메모리 사용을 줄일 수 있습니다. 
단, ref가 attach, detach될 때 어떤 코드를 실행하려 한다면 콜백 ref를 사용해야 합니다. 

<br/><br/>
# 사용법

## 1. ref 생성 

먼저 useRef 훅을 써서 컴포넌트 안에 변수를 만들어줍니다. 

![image](https://user-images.githubusercontent.com/79133602/157833045-02c1a4ed-e5eb-4783-818f-b76c71d7aca0.png)

그리고 inputRef가 조작할 dom의 ref 속성값을 inputRef로 줍니다. 
 
![image](https://user-images.githubusercontent.com/79133602/157832962-68729f14-e586-4d1e-8f35-52ec9f54c680.png)

<br/>
## 2. .current로 useRef 변수에 접근

이제 해당 input 태그에 inputRef.current로 접근이 가능합니다. (.current는 선택한 dom을 의미합니다) 만약 값이 없을 경우 해당 input tag에 focus를 주고 싶다면 아래 예시 1번처럼,
input 태그의 값에 접근하고 싶다면 아래 예시 2번처럼 코딩하시면 됩니다. 

```
inputRef.current.focus // 1번
inputRef.current.value // 2번
```

<br/><br/>
# 여러개의 dom 관리시

<br/>
만약 여러개의 dom을 조작할 때는 어떻게 해야 할까요?

<br/>
## 1. useRef를 여러개 만들기

조작해야 하는 dom 개수가 한정적이고 서로 연관성이 없는 dom 객체라면 일일이 useRef를 만들어 줘도 됩니다. 

![image](https://user-images.githubusercontent.com/79133602/157834355-dc110678-e130-4b55-b32a-9ea3a639465c.png)

이런식으로 다운받을 이미지 dom을 관리할 imgRef, input 값을 관리할 inputRef 2개를 만든 것처럼 말입니다. 

<br/>
## 2. useRef를 배열로 만들기

하지만 조작해야 되는 dom의 개수가 많고 서로 연관이 있다면 useRef를 배열로 만들어 주는 게 좋습니다. 

![image](https://user-images.githubusercontent.com/79133602/157836653-0f15ed75-b11c-49fa-be90-4c429433f7e4.png)

이렇게 배열로 useRef 변수 inputRef를 생성하고, input값이 여러개인 form에 적용해 보면

![image](https://user-images.githubusercontent.com/79133602/157837514-b0bf8e13-f739-4986-b545-85d1462edba6.png)

inputRef가 길이 3의 배열로 값이 들어간 것을 알 수 있습니다. 

<br/><br/><br/>
# 참고 

💻 [React:: hooks-reference ](https://ko.reactjs.org/docs/hooks-reference.html#useref)

💻 [벨로퍼트 모던 리액트 ](https://react.vlpt.us/basic/10-useRef.html)

💻 [useRef는 처음이라:: 개념부터 활용 예시 ](https://mnxmnz.github.io/react/what-is-use-ref/)

💻 [useRef() 여러개 dom 관리 ](https://devilfront.tistory.com/102)