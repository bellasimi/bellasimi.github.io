---
title: 
categories:
tags:
- error
- jsx
last_modified_at:
---

<br/>
리액트에서 jxs 페이지에 값을 입력하는데 다음과 같은 에러를 만났습니다.

```
jsx
react-dom.development.js:13231 Uncaught Error: Objects are not valid as a React child (found: object with keys
```

<br/>
# 원인

return문에서 {}안에 변수를 가져올 때 객체형을 넣었기 때문에 발생했습니다. jsx는 return문에 데이터를 받아올 때 {} 안에 써주는데, 객체형은 안된다고 합니다.  그래서 배열로 바꾸거나, 객체의 속성값을 가져와야 합니다. 


<br/>
# 해결

객체인 nCmt 대신 객체의 속성 값 nCmt.id에 접근하니 해결됐습니다.


```
jsx
{ cmt.nestedComments.map((nCmt, nIdx) =>
  <div key={nCmt.id}>
    {nCmt} // 객체형이라 오류남
    {nCmt.id} // 오류 안남
  </div>

)}

```


