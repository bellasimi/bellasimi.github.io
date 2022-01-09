---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- switch
- react-router-dom
last_modified_at:
---

리액트 라우터는 "/" 나 "/:id" 로 경로가 설정된 경우 모든 경로의 페이지를 라우팅합니다. 
그게 싫고 정확히 매칭된 컴포넌트만 보이게 하고 싶다면 Switch를 사용하면 됩니다. 

<br/>
# 중복을 불허

```
import {Link, Route, Switch } from 'react-router-dom';
```
먼저 사용할 페이지에서 react-router-dom 라이브러리를 import해주고 

![image](https://user-images.githubusercontent.com/79133602/148634983-5d5cf5c9-6e76-444f-9ef8-ac263570f106.png)


이렇게 라우트 태그들을 Switch 태그로 감싸주면, 이전에 모든 페이지에서 나오던 "/:id"의 내용이 사라지고 
매칭된 경로의 내용만 나오는 것을 확인할 수 있습니다.

이방법을 사용하시면 Route 태그 path앞에  일일이 exact를 적는 수고스러움을 피할 수 있습니다. 