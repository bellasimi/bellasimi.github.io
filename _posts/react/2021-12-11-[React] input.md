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



저번 시간엔 event.target 속성을 이용해 input 값을 state에 저장하는 법을 알아봤는데요. 
오늘은 그 값을 기존 state 배열에 저장해 화면해 출력하도록 해보겠습니다. 

![image](https://user-images.githubusercontent.com/79133602/145829240-51bb55a1-4073-4822-a994-914dd5faabfa.png)

위와같은 프로젝트 목록이 있습니다. 

```
let [프로젝트명, 프로젝트명변경] = useState(["BuyTicketS","Board","nodeWeb"]);
```
프로젝트명은 배열로 이뤄진 state 값인데요. 

![image](https://user-images.githubusercontent.com/79133602/145829479-844eba45-7c84-4958-9bce-8b12b1dabb28.png)

이렇게 input에 프로젝트명을 입력하고 저장을 누르면, 프로젝트 목록에 입력한 내용이 보이도록 하겠습니다. 

<br/><br/>
# input : onChange

![image](https://user-images.githubusercontent.com/79133602/145829296-8864f7f8-461d-4d6b-a8f0-2074e55e7a18.png)

input 태그엔 onChange 메소드를 이용해 값이 변할 때마다 state 값을 event.target의 value값으로 변경하도록 해줬습니다. 
만약 event.target이 뭔지 모르시겠다면 제 [전 포스트](https://bellasimi.github.io/js/JS-Event.target/)를 확인해주세요

<br/><br/>
# button : onClick

그리고 이제 저장 버튼을 누르면 onClick 메소드가 saveInput을 호출합니다. saveInput은 변수형 함수로 this를 자동으로 window로 인식해줍니다. 

<br/>
## 1. saveInput


새로운 변수를 만들어 프로젝트명 state값을 복사해주세요. ...spread 연산자를 사용해서 원본배열에 영향을 주지 않도록 합니다! 

복사본 arr에 unshift 함수를 사용해 새로운 값을 0행에 넣어준 뒤 프로젝트명변경에 arr를 넣으면 끝입니다!

```
const saveInput = () => {

let arr = [...프로젝트명]
arr.unshift(inputValue)

프로젝트명변경(arr)

```

이외에도 프로젝트명에 값을 변경하는 방법과 나쁜 방법 1가지씩 더 보여드리겠습니다.
<br/>
## 2. arr.push 사용

```
let arr = [...프로젝트명]
arr.push(inputValue)
```

<br/>

## 3. 나쁜 방법

프로젝트명에 변수에 직접 unshift 메소드를 이용해서 값을 추가할 수 있습니다. 
```

프로젝트명.unshift(inputValue)
프로젝트명변경(프로젝트명)

```

하지만 이러면 렌더링이 잘 되지 않을 수 있으니 꼭 위처럼 복사본을 만들어 변수에 저장 후 , 변수를 조작해 주셔야 합니다!!
<br/>
<br/>
# 추천 비추 기능 추가

위의 코드만으론 추천 비추 기능이 작동하지 않습니다. 

saveInput 호출 시 추천 비추 state를 변경해줘야 해당 메소드가 작동할 수 있기 때문이죠. 그래서 위 코드 아래 다음 내용을 추가해줍니다.


```
let newRepArr = [];
 for(var i=0;i<프로젝트명.length+1;i++){
    newRepArr.push(0);
 }
setGood(newRepArr)
setBad(newRepArr)

}
```

프로젝트명이 추가될 때마다 평가배열이 달라지므로 for문으로 새로 newRepArr를 만들고, 그 배열을 추천 비추 값으로 변경해주는 코드입니다. 


![image](https://user-images.githubusercontent.com/79133602/145834577-4bbdbe90-40d8-4a1e-933a-0480e46966a3.png)

그러면 이제 제대로 프로젝트명이 저장되고 추천 비추 기능이 작동하는 것을 볼 수 있습니다. 

<br/><br/><br/>

# 참조

💻 [리액트의 불변성: spread](https://unit-15.tistory.com/entry/React-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%9D%98-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%8A%A4%ED%94%84%EB%A0%88%EB%93%9C-%EC%97%B0%EC%82%B0%EC%9E%90-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%A7%80%ED%82%A4%EA%B8%B0)



