---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- useParams
last_modified_at:
---


저번 시간에 [ 반복문으로 하나의 component를 여러번 출력 ](https://bellasimi.github.io/react/React-component-+-%EB%B0%98%EB%B3%B5%EB%AC%B8/)하는 방법에 대해 알아봤습니다. 

오늘은 그렇게 만든 상품리스트를 클릭시 해당 상품의 상세페이지 경로 바꿔주는 작업을 해보도록 하겠습니다. 

<br/>
# 1. 상세페이지 라우팅

상세페이지 컴포넌트를 만들고 App.js에서 path = "/detail/:id"로 라우팅해주세요

![image](https://user-images.githubusercontent.com/79133602/149263598-c0278e8c-bcf0-4901-8202-5f4aebcedd8a.png)

그럼 /detail/ 뒤에 붙는 값을 받고 해당 값을 useParams();로 저장할 수 있습니다. 


<br/>
<br/>
# 2. /:id값 지정

전 :/id 값을 상품 데이터의 index로 지정했습니다. 

![image](https://user-images.githubusercontent.com/79133602/149264375-ea2f52eb-885d-45d6-ba32-7a06e1ec3265.png)

<br/>
## ❗ 주의점 ❗

지금은 상품리스트의 index와 상품데이터의 index가 같지만 정렬을 하면 달라집니다.

즉, :/id를 props.shoes[props.idx]라고만 하면 정렬을 할때마다 상품페이지 props.idx의 상품값이 달라지는 문제가 생깁니다.

예를 들어 기존 상품리스트[0]값이 아이폰이었는데, 가격순으로 했을 떄는 상품리스트[0]값이 갤럭시일 때
그냥 :/id를 props.shoes[props.idx]로 넘기면 갤럭시 상품을 눌렀는데 아이폰상세페이지가 나올것입니다.

그래서 정렬시에도 바뀌지 않는 고유값을 :/id로 넘기고 고유값에 index를 넣는 게 좋겠죠

![image](https://user-images.githubusercontent.com/79133602/149265214-a169e7be-ff72-4d4f-a987-b61810363444.png)

저처럼 상품데이터 객체의 id에 index값을 넣고 :/id엔 props.shoes[props.idx].id를 보내면 됩니다.

<br/>
<br/>
# 3. useParams()

자 이제 :/id로 받은 값을 링크에 넣어줄 차례인데요.

먼저 상세페이지 컴포넌트에서 라우터 라이브러리에서 useParams 훅을  import한 뒤

![image](https://user-images.githubusercontent.com/79133602/149263447-8b821a5f-c230-4ac3-86be-4cda8c1ff0d1.png)

컴포넌트 안에 아래처럼 변수선언을 해서

![image](https://user-images.githubusercontent.com/79133602/149263451-aa80dfd3-1ea6-4077-acd3-f666476e652b.png)

사용자가 입력한 url 파라미터들을 저장해주세요!

{ /:id 자리에 입력한 값 } 디스트럭쳐 문법으로 중괄호에 들어가 있음.


<br/>
<br/>
# 4. props의 인덱스로 id 사용

그리고 나서 []안에 id라고 입력하면 detail/뒤에 입력한 값이 인덱스로 들어갑니다.

![image](https://user-images.githubusercontent.com/79133602/149263457-06ce084b-41f4-43ca-bec3-3d643adc3e7c.png)

이제 해당 상품을 클릭하면 :/id로 상품데이터의 index를 받아서 해당 index의 데이터가 잘 출력되는 것을 볼 수 있습니다.

![image](https://user-images.githubusercontent.com/79133602/149265721-ca91bf06-dc00-446d-ad9d-3009cad1e5fa.png)

![image](https://user-images.githubusercontent.com/79133602/149265627-a7bf439c-d843-4c83-af15-30eabc78e240.png)
