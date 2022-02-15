---
title: 
tags:
- project
- idol_collector
last_modified_at:
---
<br/>

유효성 검사를 한 다음 검사에서 실패한 input id를 regFail state의 key값으로 넣고 value로 false를 줬다.  글씨색이 잠시동안 빨간색이 되면 좋겠어서 setTimeout()으로 5초가 지나면 다시 true가 되게 했다. 

<br/><br/>
# styled-components 조건

regFail이 false면 input에 아래와 같은 애니메이션을 주려고 한다. 

```
const warning = keyframes`
  0% { transform: translateX(-5px); }
  25% { transform: translateX(5px); }
  50% { transform: translateX(-5px); }
  75% { transform: translateX(5px); }
`
```

그리고 input placeholder 폰트색도 변경할거다.

```
const InputFailField = styled.div`
  width: 100%;
  border: 2px solid red;
  padding: 1rem 1.5rem;
  border-radius: 2rem;
  margin: 1.5rem auto;

  input {
    width:100%;
    font-size: 0.9rem;
    border: none;
    background: none;

    &:focus {
      outline: none;
    }
  }

  **input::placeholder {
    color: red;
  }
  animation: ${ warning }  1s ease;
`;**
```
<br/>
처음엔 그냥 InputFailField 컴포넌트를 따로 만들어 삼항연산자로 html에 보여질 컴포넌트를 달리하려했는데...

```
{ regFail.title ===false

? (<InputFailField>
      <input
      type="text"
      id="title"
      placeholder="카드 타이틀을 입력하세요 (10자)"
      required
      onChange={handleTitle}
      />
    </InputFailField>)
  : (<InputField>
      <input
      type="text"
      placeholder="카드 타이틀을 입력하세요 (10자)"
      required
      onChange={handleTitle}
      />
    </InputField>)
}

```

그러면 이런 코드를 5개나 더 만들어야한다 😫 너무 길고 비효율적이다. 

그래서 InputField만 가지고 조건문에 따라 위 css 설정을 주려고 한다. 

```
const InputFailField = styled.div`
  width: 100%;
  border: 2px solid red;
  padding: 1rem 1.5rem;
  border-radius: 2rem;
  margin: 1.5rem auto;

  input {
    width:100%;
    font-size: 0.9rem;
    border: none;
    background: none;

    &:focus {
      outline: none;
    }
  }

  input::placeholder {
    color: red;
  }
  animation: ${ warning }  1s ease;
`;
```

이러면 이제 해당 input이 유효성 검사에 실패해서 regFail== false일 때만  InputFailField에 해당 css가 적용된다. 근데 또 문제가 있다. 만약 input값 1객가 잘못된 경우라도  모든 InputFailField에 animation이 작동한다는 점이다.  각각 input값이 조건에 따라 달리 작동하려면 어떻게 해야 할까...

<br/><br/>
# 어쩔 리액트

리액트는 DOM 조작하지 말라그러는데 ... 한숨난다. 자바스크립트 하드코딩해서 프론트 작업할 땐 저거 그냥 docoment.querySelector() 로 가져온 input 요소 classList.toggle(’’)해서 돔 조작 후 변한 클래스명에 맞는 css를 만들면 됐는데.. 얜 어쩌라는 건지 모르겠다. 

<br/><br/><br/>
# 참조

[리액트-스타일-컴포넌트](https://velog.io/@hwang-eunji/Styled-Components-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EC%8A%A4%ED%83%80%EC%9D%BC-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)