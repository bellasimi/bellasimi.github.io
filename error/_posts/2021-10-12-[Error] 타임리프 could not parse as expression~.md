---
title: 
categories:
tags:
- error
- thymeleaf
last_modified_at:
---

오늘 만난 에러 원인은 무엇이었을까요?

![image](https://user-images.githubusercontent.com/79133602/136960344-26a4f537-4e6d-4736-acb8-174f0d453fbb.png)

parse가 안되는걸 보아 값이 잘못 입력된것 같은데요.

해당 페이지 코드를 보니 다음과 같았습니다. 

![image](https://user-images.githubusercontent.com/79133602/136960280-428c786e-2d86-42ac-a255-2bcf9d2e6d4d.png)

한참을 찾아봐도, 매핑주소값도 파람값도 잘 넣어준 것 같은데 왜그럴까 하던 도중 괄호가 잘 못 닫혀있는것을 보았습니다. 고쳐주니.. 

![image](https://user-images.githubusercontent.com/79133602/136961213-bbafe7a6-52d2-411b-a5fa-3f6da50ba010.png)

에러 없이 잘 나옵니다. 😅 여러분도 해당 에러시 값은 맞는지 또 오타가 없는지 확인해주세요.


