---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- react-router-dom
last_modified_at:
---

원래 지정 경로 페이지로 라우팅을 하려면 href를 사용했습니다. 

리액트에서도

![image](https://user-images.githubusercontent.com/79133602/148633850-9dbc7d8a-1d71-43df-b798-f0d51e150d64.png)

이렇게 입력하면 해당 페이지로 이동이 가능합니다. 

하지만 오늘은  라우터 라이브러리의 Link 기능을 사용해 이동해보도록 하겠습니다.

<br/>
# Link
  
![image](https://user-images.githubusercontent.com/79133602/148633934-f6ddd9b9-6907-4420-bfdc-9e6259430de6.png)
  
Link를 import 한 상태에서
  
![image](https://user-images.githubusercontent.com/79133602/148633943-608f8617-bfd7-472c-8e1d-44ebe737b07d.png)
  
Link 태그의 to 속성을 이용하면 되는데요.
  
![image](https://user-images.githubusercontent.com/79133602/148633953-de4c52f0-f8ae-4fca-9a07-c8d7e3c12be7.png)
  
해당 태그가 부트스트랩 네비바 기존 태그와 달라 css적용이 안됩니다. 이건 나중에 
따로 css 적용해주도록 합시다.

<br/>
# 부트스트랩 링크 중복

  
그리고 현재 Nav.Link 와 Link를 함께 쓰면 a 링크 중복이라고 부라우저 개발창에 에러메시지가 뜨는데  
이를 수정하기 위해 아래처럼 바꿔주면 됩니다.

```
<Nav.Link as = {Link} to="/detail"></Nav.Link>
```

이러면 부트스트랩 Nav.Link를 사용하면서 as 속성값 react-router-dom의 Link로 인식해 Nav.Link에서도 href가 아닌 to를 사용할 수 있습니다. 