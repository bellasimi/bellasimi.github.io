---
title: "[Error] never 형식에 click 속성이 없습니다."
categories:
tags:
  - error
  - typescript
last_modified_at:
---

![image](https://user-images.githubusercontent.com/79133602/161425228-73f31f32-57e1-492f-a341-62695d512934.png)

<br/>

## 상황

![image](https://user-images.githubusercontent.com/79133602/189565796-a7473972-b71e-4fb4-87e7-df3b673cfef9.png)

- input을 useRef를 사용해서 조작하려고 했는데, useRef.current.click() 코드에서 `never 형식에 click 속성이 없습니다.`라는 에러를 만나게 됐습니다.

<br/>

## 원인

**useRef를 타입스크립트**에서 사용할 때 **제너릭을 명시하지 않고 빈 값을 넣으면 never 타입**이 됩니다.

never 타입은 **어떠한 값도 가질 수 없으며** any 타입과 다릅니다. **일반적으로 함수의 리턴 타입으로 사용**되는데 이 경우, **항상 오류를 출력하거나 리턴 값을 절대로 내보내지 않습니다.**

<br/>

## 해결

useRef가 사용되는 곳의 타입을 제너릭에 명시해 줘야 합니다.

![image](https://user-images.githubusercontent.com/79133602/189565830-046bd705-6303-4c1a-b86c-3ed1bfe53b22.png)

<br/><br/><br/>

# 참고

💻 [React에서 TypeScript 적용하기 & 오류 해결하기](https://velog.io/@dosilv/TypeScript-React%EC%97%90%EC%84%9C-TypeScript-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0)
