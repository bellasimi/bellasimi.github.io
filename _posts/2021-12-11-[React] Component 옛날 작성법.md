---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- js
last_modified_at:
---

요즘엔 함수로 컴포넌트를 생성하고 useState를 이용해 값을 저장하지만 

옛날엔 클래스로 컴포넌트를 생성하고 생성자함수안에 this.state에 값을 저장했습니다. 

물론 이제 그런식으로 코딩할 일을 없겠죠. 

그러나, 유지 보수를 하다보면 옛날 코드를 마주할 때가 있습니다. 오늘은 그런 때를 대비해 구형 컴포넌트 작성법을 보도록 하겠습니다.  


# class 생성

먼저 React의 component만드는 클래스를 상속해 클래스를 만들어 줍니다. 

```
class Profile extends React.Component {
    constructor(){
        super();
        this.state = {name : 'Hah', age : 99}
    }
}
```

그다음 생성자 함수를 만들어 주고, 그 안에 해당 클래스에서 사용할 state 변수값을 입력해줍니다.

현대식 문법이 useState() 메소드를 사용해 객체를 각각 다른 변수에 넣어 관리해주는 것과 달리 모든 값을 this.state 하나의 변수에 담아 사용합니다.

꼭 this를 붙여서 전역을 참조하도록 해주세요!




생성자함수 아래 render 함수를 이용해 웹상에 띄울 html 문서를 return하도록 코드를 짜줍니다. 

```
    render(){
        return(
            <div>
                <h1>옛날 방법 컴포넌트 만들기</h1>
                <li>이름 : {this.state.name}</li>
                <li>나이 : {this.state.age}</li>
                <button onClick={ ()=> {this.setState({name:'Choi'})}}>이름변경</button>
                <button onClick={()=>{ this.changeAge.bind(this) }}>나이변경</button>
            </div>
        )

    }

```

# state 변경

여기서 state값을 사용하기 위해선 {} 안에 변수명을 입력하면 되는데, 
값을 변경하고 싶을 때는 setState()를 써서 this.state의 특정 객체만 따로 수정하는 것도가능합니다. 

현대식 문법이 값의 일부만 변경하기 번거로운데 비해 이런점은 편리하네요.

만약 함수를 따로 빼서 사용하고 싶다면 

```
    changeAge(){
        this.setState({age : 19})
    }

```
이런식으로 render()위에 코딩을 하고 return문의 jsx문법으로 불러오면 되는데요. 


한가지 주의할 점이 있습니다. 


자바스크립트에서 변수는 this를 window 즉 전역으로 인식하고,

함수는 해당함수 내의 지역안에서 인식합니다. 


따라서 changeAge 함수를 onClick에서 호출할 때 그냥 this.changeAge라고 불러오면
changeAge안의 값 this.setState({age:19})이 전역을 참조하지 못 해 에러가 납니다. 

꼭 bind(this)함수를 써서 전역을 인식하게 해주세요. 

만약 bind(this)함수를 쓰기 싫다면 changeAge 함수를 변수화해서 사용해주세요. 

```
     changeAge = () => {
            this.setState({age : 19})
        }
```


