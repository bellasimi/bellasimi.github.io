---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- useHistory
- react-router-dom
last_modified_at:
---

useHistory는 방문기록을 저장할 수 있는 기능으로 훅으로 객체를 초기화해서 사용하는데 뒤로가기 같은 기능에 사용하기 좋습니다.

<br/>
<br/>
# 사용방법

```
import { useHistory } from 'react-router-dom';
```
먼저 react-router-dom 라이브러리를 import할 때 useHistory를 받아옵니다. 

```
let history = useHistory();
```
그리고 객체에 담아준 뒤 아래 함수들 필요에 따라 사용해 주시면 됩니다. 

<br/>
## goback() : 뒤로가기

```
<button onClick={()=>{history.goBack()}}>주문취소</button>
```

History의 goback() 메소드를 넣어 코딩하면 주문취소를 눌렀을 때 이전페이지로 이동합니다. 

<br/>
## push() : 해당 경로로 이동

```
<button onClick={()=>{history.push("/anywhere")}}>이동</button>
```

해당 경로로 지정된 페이지로 라우팅해줍니다. 

❗ 만약 위 명령어가 작동하지 않는다면 라 react-router-dom가 잘 설치가 됐는지 버전이 v5이상인지 그리고 react 버전은 v16.3이상인지 확인해주세요 ❗ 