---
title: "[Error] React dom custom 속성 에러"
categories:
tags:
  - error
  - typescript
last_modified_at:
---

![image](https://user-images.githubusercontent.com/79133602/161425228-73f31f32-57e1-492f-a341-62695d512934.png)

<br/>

## 상황

```js
type IconType = {
  isActive: boolean,
};

<StyledHome isActive={pathname === HOME_URL} />;

const StyledHome =
  styled(BiHomeAlt) <
  IconType >
  `
  width: 3rem;
  height: 3rem;
  color: ${({ isActive }) => isActive && theme.color.mainPink};
`;
```

아이콘에 isActive라는 커스텀 속성을 부여해서 만약 pathname이 home이면 아이콘의 색이 변경되도록 처리하려고 했는데 다음과 같은 에러를 만났습니다.

![image](https://user-images.githubusercontent.com/79133602/189568051-112d7689-11a6-4558-9a5e-d0089bc02812.png)

<br/>

## 원인

emotion styled을 적용한 dom에 커스텀 속성을 부여하려면 속성명을 소문자로 바꿔줘야 합니다.

따라서 다음과 같은 코드로 해결할 수 있습니다.

```js
type IconType = {
  isactive: boolean,
};

<StyledHome isactive={pathname === HOME_URL} />;

const StyledHome =
  styled(BiHomeAlt) <
  IconType >
  `
  width: 3rem;
  height: 3rem;
  color: ${({ isactive }) => isactive && theme.color.mainPink};
`;
```

## 또 다른 문제

위 방법으로 lower case 에러를 벗어났지만, 여전히 에러가 발생합니다. isactive 속성은 boolean을 사용할 수 없다는 메시지 입니다.

![image](https://user-images.githubusercontent.com/79133602/189569020-6d6da0b9-4b67-4181-ae87-f0e6fb874757.png)

해당 에러를 해결하기 위해선 다음과 같이 코드를 수정해야 합니다.

```js
type IconType = {
  isactive: boolean,
};

<StyledHome isactive={pathname === HOME_URL ? 1 : 0} />;
```

<br/>

## 더 나은 해결

하지만 위 방법 모두 가독성이 떨어지고 에러가 나지 않는다면 절대 사용하지 않을 어색한 문법입니다. 따라서 커스텀 속성 대신, 다음과 같이 boolean이 가능한 지정된 속성값을 사용하는 게 훨씬 좋습니다.

```js
type IconType = {
  selected?: boolean,
};

<StyledHome selected={pathname === HOME_URL} />;

const StyledHome =
  styled(BiHomeAlt) <
  IconType >
  `
  width: 3rem;
  height: 3rem;
  color: ${({ selected }) => selected && theme.color.mainPink};
`;
```

<br/><br/><br/>

# 참고

💻 [styled-components DOM issue](https://velog.io/@young_pallete/Styled-components-DOM-issue)
