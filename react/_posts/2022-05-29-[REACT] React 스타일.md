---
title: "[REACT] React 스타일"
categories:
  - react
tags:
  - react
toc: true
toc_sticky: true
---

![image](https://user-images.githubusercontent.com/79133602/161557696-fe3b688d-f6d2-4073-a18f-8d57377acaa7.png)

<br/>

# 리액트 스타일 적용

1. css 파일 사용
2. inline 스타일 적용
3. emotion 라이브러리

# emoition

> yarn add @emotion/react @emotion/styled

(emotion 설치문서)[https://emotion.sh/docs/install]

> yarn add --dev @emotion/babel-plugin (CRA는 안돼)

babelrc를 만들어서 사용하라고는 하는데 create-react-app에선 적용이 안된다 그럴 땐 다음 방법을 사용하면된다.

## 1. 프레그마

> 파일에게 컴파일러가 어떻게 처리하는 알려줌

페이지 상단에 아래 코드를 입력해주면 된다. 이는 현재 react의 jsx를 사용해서 emotion의 jsx로 자동변환되지 않기 때문이다. 이 프레그마는 babel이 jsx를 변환할 때 React.createElement 대신 emotion의 jsx 함수를 사용하게 해준다.

```js
/* @jsxImportSource @emotion/react */
```

## 2. CRACO: Create React App Config Override

> yarn add -D @craco/craco
> yarn add @emotion/babel-preset-css-prop

craco는 cra 설정이 가능하게 해주는 라이브러리다.
설정을 오버라이딩해서 사용 -> craco.config.js 파일을 만들어서 module.expors = {여기에 바벨 설정을 넣어줄 수 있다.}

```js
module.exports = {
  babel: {
    presets: ["@emotion/babel-preset-css-prop"],
  },
};
```

<br/><br/>

# emotion을 써야하나?

@emotion 패키지를 쓰려면 프래스마 또는 yarn add --dev @emotion/babel-plugin 바벨 설정을 해줘야 되는데 이게 CRA에서 먹히지 않아서 CRACO를 통해 설정을 오버라이딩해주고 있다. styled-component를 쓰면 해당 설정을 해주지 않아도 되는데 emotion을 써야 할까?

<br/>

# emotion VS styled-component

![image](https://user-images.githubusercontent.com/79133602/170831346-7feaa699-de10-409d-aa55-40a1551950d3.png)

일단 사용량은 styled-component가 우세하다고 한다.

![image](https://user-images.githubusercontent.com/79133602/170831380-93e953b2-97f4-4692-95a6-c3d079fd1c66.png)

하지만 npm 다운로드 횟수는 emotion이 앞선다.

### 용량, 속도 모두 emotion이 style-component보다 낫다.

https://bundlephobia.com/에서 두 라이브러리를 검색해보면 emotion이 style-component보다 용량이 작다는 걸 알 수 있다. 다만 emotion은 @emotion/react, @emotion/styled 두개 다 설치해야 되기에 이땐 비슷하다. 그렇다고 해도 속도는 여전히 emotion이 낫다. [css 라이브러리 속도 비교](https://github.com/A-gambit/CSS-IN-JS-Benchmarks/blob/master/RESULT.md)를 보면 근소하게 빠르다.

### SSR을 쓴다면 emtion이 낫다.

emotion은 SSr에서 별도의 설정이 없어도 동작이 되지만 styled-components의 경우 [ServerStyleSheet](https://styled-components.com/docs/advanced#streaming-rendering)을 설정해 줘야 한다.

### TypeScript 역시 emotion이 낫다.

styled-components는 타입스크립트를 미지원하기 때문에 @types/styled-components 를 설치하고 \_document.tsx 파일을 작성해야 한다. 하지만 emotion의 경우 추가적인 패키지 설치나 파일 작성이 필요없다.

<br/>

## @mui/material UI디자인 프레임워크만 사용한다면?

이경우엔 @emotion, styled-components 둘 다 필요 없다고 생각한다. 공식문서에도 나와 있듯이 @mui/material/styles 라이브러리의 styled만으로 해당 컴포넌트의 세부 style을 커스터마이징 할 수 있기 때문이다.

```
import * as React from 'react';
import Slider from '@mui/material/Slider';
import { styled } from '@mui/material/styles';

const CustomizedSlider = styled(Slider)`
  color: #20b2aa;

  :hover {
    color: #2e8b57;
  }
`;

export default function StyledComponents() {
  return <CustomizedSlider defaultValue={30} />;
}

```

<br/><br/>

# 결론

> MUI + emotion

타입스크립트를 추후 적용할 예정이고 모든 컴포넌트를 MUI로 만들지 않을 것이기 때문에 @emotion 라이브러리를 사용해야겠다. 그리고 MUI에선 @mui/material/styles의 styled를 사용해 커스터마징을 해야겠다.

<br/>

# 참고

💻 [프로그래머스](https://programmers.co.kr/?utm_source=google&utm_medium=cpc&utm_campaign=brand_prgms_pc&gclid=CjwKCAjwp7eUBhBeEiwAZbHwkekJzz--rpwSreONc8ae4HmHJ1sGO2bEJnbt7JZgGJOzKoCScBj2xhoC6BIQAvD_BwE)

💻 [MUI styled 사용방법](https://mui.com/material-ui/guides/interoperability/#styled-components)

💻 [emotion css props](https://emotion.sh/docs/css-prop)

💻 [타입스크립트 이모션조함 props 넘기기](https://namunamu1105.medium.com/react-js-typescript-emotion-js-%EC%A1%B0%ED%95%A9%EC%97%90%EC%84%9C-emotion-js%EC%97%90-props%EB%84%98%EA%B8%B0%EB%8A%94-%EB%B2%95-5e1ab7a33f8c)

💻 [next.js + emotion + MUI](https://velog.io/@ckm960411/Next-TypeScript-%EB%84%A5%EC%8A%A4%ED%8A%B8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-Material-UI-styled-components-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0-emotion-%EC%94%81%EC%8B%9C%EB%8B%A4)
