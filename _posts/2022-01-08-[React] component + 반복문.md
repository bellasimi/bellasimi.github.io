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

쇼핑몰의 메인페이지엔 상품 수 만큼의 상품컴포넌트들이 출력됩니다. 그런데 이 코드들을 일일이 입력한다면... 😱 너무 일이 많아질 것입니다.


# 반복문 출력

그래서 반복되는 내용을 map() 메소드를 이용해서 여러번 출력합니다. 그리고 값은 배열에 객체로 담아 각각의 인덱스마다 해당 값이 출력될 수 있도록 합니다. 

예를 들어 다음과 같은 data 변수가 있고 그 값을 Device라는 컴포넌트에서 출력할 때

![image](https://user-images.githubusercontent.com/79133602/148945264-7438abe9-d22d-4d98-997d-5fac465b9619.png)

Device 컴포넌트를 data 변수 데이터 양만큼 map() 메소드를 사용해 반복문을 돌려주고 

![image](https://user-images.githubusercontent.com/79133602/148945098-bac81368-df39-4e25-9f54-13612332d6f8.png)

반복문 내 함수에서 매개변수로 each(각행의 값), idx(행인덱스)를 받아서 props로 Device 컴포넌트로 보내면
해당 컴포넌트에서 각행의 값을 출력합니다. 

![image](https://user-images.githubusercontent.com/79133602/148945128-44386d44-e507-41f4-b0a8-d831b6564ab4.png)


그러면 쇼핑몰 메인 페이지 상품컴포넌트를 일일이 입력하지 않아도 되서 가독성도 좋고 효율적이죠

# 주의점

반복문에서 값을 보낼 때 key값으로 고유값을 넘겨줘 식별이 가능하도록 해줍니다.

![image](https://user-images.githubusercontent.com/79133602/148945964-72890339-085a-437d-a8b3-0ce944201b51.png)

