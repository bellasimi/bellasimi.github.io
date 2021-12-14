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

App이란 컴포넌트에 아래 변수가 있습니다. 

```
let [modalTitle,setModalTitle] = useState("모달 제목");
let [modalIdx,setModalIdx] = useState(0);
let [프로젝트명, 프로젝트명변경] = useState(["BuyTicketS","Board","nodeWeb"]);
```

다른 컴포넌트에서 이 변수들을 사용하고 싶을 때 어떻게 하면 될까요? 🤔

<br/>
<br/>
# props 사용


먼저 props를 사용하지 않고 그냥  바로 값을 넘기면 오류가 나는 걸 보실 수 있습니다.

```
function Modal(props){
    return (
        <div className="modal">
            <h2>{modalTitle}</h2>
            <p>날짜</p>
            <p>상세내용</p>
            <p>{프로젝트명[modalIdx]}</p>
        </div>
    );
}

```

다른 component의 변수를 받기 위해선 component 함수에서 props를 매개변수로 받아 원하는 변수에 접근하면 됩니다. 

그러기  위해선 App 컴포넌트에서 props를 전송해주는데


```
{ modal === true
  ? <Modal modalTitle={modalTitle} modalIdx={modalIdx} 프로젝트명={프로젝트명}/>
  : null
}
```

이렇게 state를 어떤 이름으로 넘겨줄지 컴포넌트 태그 안에 작명하고

> <컴포넌트명 작명={전송할 state명}/> 

해당 컴포넌트 함수에서 {props.작명} 으로 state에 접근합니다. 


```
function Modal(props){
    return (
        <div className="modal">
            <h2>{props.modalTitle}</h2>
            <p>날짜</p>
            <p>상세내용</p>
            <p>{props.프로젝트명[props.modalIdx]}</p>
        </div>
    );
}

```

프로젝트명의 경우 배열의 값이라 index를 modalIdx로 넘겨줬는데, 이때도 props.modalIdx로 입력을 해줘야 오류가 나지 않습니다.


