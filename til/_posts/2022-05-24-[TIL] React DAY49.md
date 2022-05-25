---
title: "[TIL] React DAY49"
categories:
  - til
tags:
  - til
  - react
toc: true
toc_sticky: true
---

![image](https://user-images.githubusercontent.com/79133602/161557696-fe3b688d-f6d2-4073-a18f-8d57377acaa7.png)

<br/>

# 오늘 새로 알게 된 부분

- jsx에서 class가 아닌 className을 사용하는 이유는 class가 js의 예약어이기 때문이다.

## useRef 지역변수로 사용?

1. DOM에 직접 접근할 때 사용

2. 지역 변수로 사용 재렌더링 안할 때 <-> useState는 값 변할 때 재렌더링

   useState는 값이 변경되면 다시 렌더링하지만 useRef는 값이 변경되더라도 다시 렌더링하지 않는다.
   그래서 변수처럼 사용하면 해당 변수값이 바뀌어도 재렌더링이 일어나지 않는다.

예로 다음 코드에서 intervalId는 useRef()로 current 값이 바뀌는 와중에도 재렌더링이 없다!

```js
import { useState, useRef } from "react";

const AutoCounter = () => {
  const [count, setCount] = useState(0);
  const intervalId = useRef();

  const handleStart = () => {
    intervalId.current = setInterval(() => {
      setCount((count) => count + 1);
    }, 1000);
  };

  const handleStop = () => {
    clearInterval(intervalId.current);
  };

  return (
    <>
      <div>{count}</div>
      <button onClick={handleStart}>Start</button>
      <button onClick={handleStop}>Stop</button>
    </>
  );
};

export default AutoCounter;
```

<br/><br/>

# 알고 있었지만 중요한 부분

## 1. 하나의 컴포넌트는 fragment로 묶인 상태여야 함

<> </> <eact.Fragment> </React.Fragment> 이런식으로 묶기

## 2. if같은 조건문은 쓸 수 없다!

{} 안에는 if 조건문이 올 수 없다 그래서 삼항연산자, &&로 렌더링 조건 부여한 뒤 해당 내역이 출력 되도록 한다.

## 3. 자바스크립트 변수는 {}에 담아서 사용가능

가상돔이기 때문에 성능 최적화 따로 안 해도 빠름

## 4. props의 기본값 지정

PropTypes 라이브러리를 사용하면 매개변수로 들어오는 props의 기본값과 타입을 객체형으로 지정할 수 있다.

```js
import logo from './logo.svg'
import PropTypes from 'prop-types'

function Logo(props) {
  return (

  )
}

Logo.defaultProps = {
  size: 200,
}

Logo.propsTypes = {
  size: PropTypes.number,
}

```

만약 이보다 간단한 형태로 만들고 싶다면 비구조화 할당을 사용하면 된다.

```js
import logo from './logo.svg'

function Logo({ size = 200 }) {
  return (

  )
}
```

## 5. 컴포넌트 태그 안의 값을 가져오려면?

> children

```js
<Paragragh>
  Edit <code>src/App.js</code> and save to reload.
</Paragragh>
```

```js
function Paragragh({ children, size }) {
  return <p style={{ fontSize: size }}>{children}</p>;
}
```

만약 children의 기본값과 타입을 지정하려면 children: PropTypes.node 노드타입으로 가져오고 필수 값이라면 .required를 붙인다.

```js
Paragraph.propTypes = {
    size: PropTypes.number
    children: PropTypes.node (만약 필수값이라면 + .required)
}
```

## 6. useEffect 사용 법

> state의 변화 감지

```js
useEffect(() => {
  //state의 값이 변경되면 여기 적힌 코드를 실행함
}, [state]);
```

> life cycle처럼 활용가능

```js
useEffect(() => {
  //[] 안에 아무것도 적지 않으면 처음 로드될 때만 여기 적힌 코드 실행
}, []);
```

만약 컴포넌트 로드시 이벤트를 주고 컴포넌트 제거시 이벤트를 삭제하고 싶다면 다음과 같이 하면 된다.

```js
useEffect(() => {
  const handleScroll = () => {
    console.log(`스크롤 이벤트 발생 ${window.scrollY}`);
  };

  document.addEventListener("scroll", handleScroll);
  return () => document.removeEventListener("scroll", handleScroll);
}, []);
```

useEffect안 return문은 컴포넌트가 제거될 때 실행되는 코드들이다. 그래서 위 코드에서 문서에 걸린 scroll 이벤트는 컴포넌트가 제거됐을 때 함께 제거된다.

<br/><br/>

# 궁금증

> PropTypes VS TypeScript

prop의 타입을 PropTypes으로 테스트하고 있는데 TypeScript로 대체할 수 있다. 어떤 방식을 현업에서 선호하는 지 궁금했는데, 현업에선 자바스크립트 + PropTypes를 많이 쓴다고 한다. 다만, 이게 더 효율적이고 좋아서 쓴다기 보다 타입스크립트의 진입장벽이 높아서 이 방법을 쓰는 거라 팀원들이 타입스크립트를 잘 다룬다면 타입스크립트를 쓰도록 해야 겠다.

<br/><br/><br/>

# 5 참고

💻 [프로그래머스](https://programmers.co.kr/?utm_source=google&utm_medium=cpc&utm_campaign=brand_prgms_pc&gclid=CjwKCAjwp7eUBhBeEiwAZbHwkekJzz--rpwSreONc8ae4HmHJ1sGO2bEJnbt7JZgGJOzKoCScBj2xhoC6BIQAvD_BwE)
