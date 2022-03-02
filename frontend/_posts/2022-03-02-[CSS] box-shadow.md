---
title: 
sidevar:
  nav: "docs"
categories:
- css
tags:
- css
- box-shadow
last_modified_at:
---

box-shadow는 선택한 요소에 그림자 효과를 만들어 주는 css 속성입니다.
기본값은 none으로 그림자 효과가 없는 상태입니다.

<br/><br/>
# 사용법

> box-shadow: x축 y축 blur spread color


x축 : 오른쪽, 왼쪽 그림자 효과를 줍니다. 양수일 경우 오른쪽에 음수일 경우 왼쪽에 그림자가 생깁니다. 

<br/>
y축:  위, 아래 그림자 효과를 줍니다. 양수일 경우 아래쪽에 음수일 경우 위 쪽에 그림자가 생깁니다.
 
<br/>
blur: 그림자에 번짐효과를 줍니다. 값이 클 수록 흐릿하게 보입니다. 

<br/>
spread: 그림자의 크기를 설정합니다. 

<br/>
color: 그림자 색을 설정합니다. 

<br/>
inset: 그림자가 안쪽에 생깁니다.

<br/><br/>
# 사용 예


변경전엔 hover css가 없었기 때문에 카드 리스트에 마우스를 대도 변화가 없습니다.

```
const Card = styled.li`
  display: inline-block;
  padding: 0.4rem;
  width: 100%;
  border-radius: 10px;

  img {
    border-radius: 10px;
    width: 100%;
  }

`;
```


hover css 추가 후엔 마우스를 카드 리스트에 올리면 padding이 사라져 img가 확대되고 img의 display를 block으로 바꿔서 여백없이 해당 Card 리스트에 꽉 차도록 했습니다.
그리고 box-shadow 효과를 줘 그림자가 생기는 것을 볼 수 있습니다. 

```
const Card = styled.li`
  display: inline-block;
  padding: 0.4rem;
  width: 100%;
  border-radius: 10px;

  img {
    border-radius: 10px;
    width: 100%;
  }

  &:hover {
    padding: 0;
    box-shadow: 4px 4px 10px grey;
    img {
      display: block;
    }
  }

`;
```

![Idol-Collector-Chrome-2022-03-02-21-47-49](https://user-images.githubusercontent.com/79133602/156365741-88242664-e69b-4e10-b8ed-2341569e19e7.gif)


<br/><br/><br/>

# 참고

💻 [MDN 사이트](https://developer.mozilla.org/ko/docs/Web/CSS/box-shadow)

