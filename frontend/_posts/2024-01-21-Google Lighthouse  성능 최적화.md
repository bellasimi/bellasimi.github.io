---
title: "Google Lighthouse 성능 최적화"
categories:
  - Google Lighthouse
  - 최적화
toc: true
toc_sticky: true
---

### Google Lighthouse로 성능 측정

여러 페이지를 가지고 성능 검사를 해본 결과, 공통적으로 LCP가 크고, 화면 로딩에 오랜 시간이 소요되는 문제가 있었습니다.
![image](https://github.com/bellasimi/bellasimi/assets/79133602/9d4d2d63-46e0-43d2-9662-705c65599f52)

<br/>

### LCP란

가장큰 요소가 페인팅에 걸리는 시간으로, 화면이 얼마나 빠르게 보이는 지 파악할 수 있습니다. 4초 이상인 경우, 사용자 경험을 심각하게 해치기 때문에 그 이하로 맞추기 위한 노력이 필요합니다.

![image](https://github.com/bellasimi/bellasimi/assets/79133602/769ae85f-a6de-4cc1-8855-883586fa9522)

![image](https://github.com/bellasimi/bellasimi/assets/79133602/e5c1512f-4619-4614-8dc6-abc7deb25d58)

<br/>

### LCP가 나쁜 원인

페이지 렌더링 시 해당 페이지에서 사용하지 않는 모듈까지 로드를 하고 있었기 때문에 속도가 나빴습니다. 아래 보시면 렌더링 지연에 시간이 너무 많이 소요되는 데, 이는 js 모듈을 로드할 때까지 기다리기 때문입니다.

![image](https://github.com/bellasimi/bellasimi/assets/79133602/ebf02188-ea91-4af0-8f45-f36f70e8778a)

문제는 해당 js를 페이지에서 사용하지 않기에, 로드할 필요가 없다는 점이었습니다. 파일 내용을 보면, 제가 예시로 측정한 페이지에서 사용하지 않는 react-icon이 로드되고 있습니다.

![image](https://github.com/bellasimi/bellasimi/assets/79133602/a0cdae70-a5f0-48f3-aac0-251854e5f862)

로드된 모듈을 확인해보니, 리액트 아이콘 전체를 가져오고 있었습니다.

![image](https://github.com/bellasimi/bellasimi/assets/79133602/bb0ca7e5-b03f-42fc-b98b-786e58c92ca6)

<br/>

### 해결 방법

다음과 같이 lazy loading, tree-shaking으로 필요한 모듈만 로드하도록 처리하면 됩니다.

1. lazyLoading : 해당 페이지에서 필요한 모듈만 가져오면 되기에, 페이지를 lazy 메서드로 import 하도록 수정해줍니다.

   ```jsx
   const MyPage = lazy(() => import("./pages/Mypage"));
   const SettingPage = lazy(() => import("./pages/SettingPage"));
   const EditorPage = lazy(() => import("./pages/EditorPage"));
   const LoginPage = lazy(() => import("./pages/LoginPage"));
   ...생략
   ```

2. 또, tree shaking을 지원하는 라이브러리 `@react-icons/all-files` 로 아이콘을 가져와 쓰도록 합니다.

   ```jsx
   import { IoClose } from "@react-icons/all-files/io5/IoClose";
   ```

<br/>

### 결과

`LCP`가 약 **30% 감소**, `Total Blocking Time`이 약 **90% 감소**

**성능**이 약 **2배 개선**된 것을 확인할 수 있었습니다.

![image](https://github.com/bellasimi/bellasimi/assets/79133602/8043bfb1-19d2-435d-bea6-fa356a89eb82)
