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
component를 사용하면 여러줄의html을 한 단어로 줄여서 쓸 수 있습니다. 
리액트에선 하나의 주제값을 보여주는 div를 만들 때 컴포넌트형태로 만드는데요. 
쇼핑몰 화면 각각의 상품칸이 이런 형태를 띄고 있다고 생각하시면 됩니다. 

<br/>
예를 들어 아래 코드를 전부 입력한다면 return 해줘야되는 html문서는 div 지옥이 될겁니다. 😥

```
                <div className="modal">
                    <h2>제목</h2>
                    <p>날짜</p>
                    <p>상세내용</p>
                </div>
```

이코드대신 component를 사용하면

```
<Modal></Modal> 
```

또는 <Modal />이렇게 간결해지는 거죠! 😎


<br/>
<br/>

# compontent 만들기


먼저 index.html에 랜더링을 하고있는 컴포넌트 App() 메소드 밖에 다음과 같이 함수를 만들어 줍니다. 

```
function Modal(){
    return (
        <div className="modal">
            <h2>제목</h2>
            <p>날짜</p>
            <p>상세내용</p>
        </div>
    );
}
```
함수명은 당연히 component의 이름이 되야겠죠, 저는 Modal로 지정했습니다.
그리고 App()의 return문 html 문서에서 원하는 위치에  <Modal />이런식으로 입력하면 되는데

조건에 따라 보이도록 하고 싶다면 다음과 같이 해주시면 됩니다. 


<br/>
<br/>

# 조건문으로 component 조작

일단 조건이 될 값을 state에 저장해줍니다. 보통 true false로 값을 지정해 스위치를 만들어줍니다. 

```
   let [modal,setmodal] = useState(true); 

```

그리고 이값에 따라 Modal이 보이도록 코드를 짜주면 되는데요. 

JSX에서 if문은 {}안에 들어갈 수 없기 때문에 대신 삼항 연산자를 써주셔야 합니다. 


```
{
   modal === true
	? <Modal/>
	: null;// 텅빈 HTML이라는 뜻
}

```


저는 값과 자료형을 모두 비교하기 위해 ===연산자를 썼는데요. 
어짜피 false, true를 state값으로 넣어주시는 경우라면 값만 비교하는 == 연산자를 사용하셔도 됩니다.

<br/>
<br/>


# Component 유의사항

* 이름은 대문자로 시작 

* return() 안에 내용을 전부 묶는 단 하나의 가 있어야 함  <div> 쓰기 싫으면 <></>사용 

* 위치는 사용할 function 밖에 생성 


<br/>
<br/>
#  Component 만드는 기준

* 반복 출현하는 HTML 덩어리들

* 자주 변경되는 HTML UI들

* 다른 페이지 만들 때 


<br/>
<br/>
# 장단점 


* 장점 : 가독성이 좋고 효율적인 코딩 가능 

* 단점 : 많아지면 state 쓸 때 복잡함


```
function Modal(){
    return (
        <div className="modal">
            <h2>{ App()에 선언한 변수 }</h2>
            <p>날짜</p>
            <p>상세내용</p>
        </div>
    );
}
```

이렇게 사용 못 함  -> props 문법 사용해야 함







