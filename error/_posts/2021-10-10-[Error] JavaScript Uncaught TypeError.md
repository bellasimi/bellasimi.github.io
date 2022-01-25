---
title: 
categories:
tags:
- error
- js
last_modified_at:
---


![image](https://user-images.githubusercontent.com/79133602/136665431-4bd0ba6a-fe8b-4068-a112-977e35dae349.png)


자바스크립트를 사용하다 보면 이런 에러를 많이 보셨을겁니다! 의외로 자주 뜨는 에러로 저의 경우 아래와 같지만, 
아마 다른 분들도  Uncaught TypeError: Cannot read () of null 에서  ()만 다를거에요.

```
requiredWarning.js:21 Uncaught TypeError: Cannot read properties of null (reading 'value')
```

<br/>
# 원인

HTML이 모두 해당 태그를 참조할 수 없어서 에러가 발생한것입니다. 원래 자바스크립트는 html보다 먼저 읽히는데 해당 태그값을 못찾으니 null을 참조하게되는거죠




<br/>
<br/>
# 헤결방법 

head안의 자바스크립트영역을 body태그 아래에 위치시켜주세요. 
만약 계속 head안에 자바스크립트 영역을 두고 싶으시다면 스크립트 태그 안에 defer를 추가해주세요.

![image](https://user-images.githubusercontent.com/79133602/136665833-b0db3a76-06a8-486e-83e5-5e6b6284ff02.png)




<br/>
<br/>
<br/>
# 참고

💻 [https://stackoverflow.com/questions/](https://stackoverflow.com/questions/22057610/uncaught-typeerror-cannot-read-property-value-of-null)