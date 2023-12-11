---
title: "useHydratedStore - Next.js React Hydration Error 방지"
categories:
  - useHydratedStore
  - zustand
  - next.js
  - clean-code
toc: true
toc_sticky: true
---

### React Hydration Error

Next.js에선 SSR에서 만든 React tree와 CSR에서 만든 React Tree가 일치하지 않을 때 에러가 발생합니다. 해당 에러는 pre-rendering된 html에 hydration으로 script를 적용할 때 발생하기에 `React Hydration Error`라고 부릅니다. 일치하지 않는 원인은 당연히 Client에서만 동작하는 코드가 있기 때문입니다.

<br/>

### React Hydration Error 원인들 예시

대표적으로 Client에서만 동작하는 코드는 다음과 같습니다.

1.  `typeof window !== 'undefined'` 조건문
    window는 Client에만 존재하는 API입니다. 해당 조건문은 Client일때만 동작하기에 SSR과 차이를 만듭니다.
2.  browser-only APIs like window or localStorage
    1번과 마찬가지로 Client에만 존재하는 browser API들 관련 코드들 역시 에러의 원인입니다.
3.  time-dependent APIs such as the Date() constructor
4.  그외, HTML을 조작하는 script 코드가 있는 경우

<br/>

### 그렇다면 어떻게 해결할까?

해결방법은 간단합니다. 원인이 되는 코드를 CSR일 때만 나타나도록 하면 됩니다. 그러기 위해 세가지 방법이 있는데요.

1. 컴포넌트를 import할 때 SSR이 안되도록 함
   이 방법은 컴포넌트 자체가 CSR에만 나타납니다. SEO 최적화에 굳이 필요하지 않고, 해당 컴포넌트의 핵심기능이 SSR 지원이 되지 않을 떄 사용할 수 있습니다. 저같은 경우 에디터편집기 컴포넌트를 이런식으로 import해서 사용했습니다.

   ```jsx
   import dynamic from "next/dynamic";

   const NoSSR = dynamic(() => import("../components/no-ssr"), { ssr: false });

   export default function Page() {
     return (
       <div>
         <NoSSR />
       </div>
     );
   }
   ```

2. time요소의 경우 - `suppressHydrationWarning` 를 true로 주기
   ```jsx
   <time datetime="2016-10-25" suppressHydrationWarning />
   ```
3. useEffect로 CSR를 감지하고 CSR일 때만 화면에 표시하도록 하기
   script에 따라 html값이 변하는 경우 아래처럼 isClient flag 값에 따라 script값을 사용할지 정해주면 됩니다.

   ```jsx
   import { useState, useEffect } from "react";

   export default function App() {
     const [isClient, setIsClient] = useState(false);

     useEffect(() => {
       setIsClient(true);
     }, []);

     return <h1>{isClient ? "This is never prerendered" : "Prerendered"}</h1>;
   }
   ```

<br/>

### 실제 해결사례: Zustand를 적용하다 만난 React Hydration Error

Zustand로 다음과 같이, 사용자의 기본 정보를 localStorage에 저장후 추가로 서버에 API를 호출하지 않도록 구현했는데요. Zustand Store는 Client에만 존재하기에, React Hydration Error가 나타납니다.

```js
import { Role } from "@/types/Role";
import { create } from "zustand";
import { persist } from "zustand/middleware";

export interface User { ...생략}

export interface UserStore {
  user: User;
  setUser: (user: User) => void;
  clearUser: () => void;
  updateUserBy: (
    userNames: Pick<User, "name" | "firstName" | "lastName">,
  ) => void;
}

const useUserStore = create<UserStore, [["zustand/persist", UserStore]]>(
  persist(
    (set) => ({
      user: INITIAL_USER,
      setUser: (user) => set(() => ({ user })),
      clearUser: () => set(() => ({ user: INITIAL_USER })),
      updateUserBy: (userNames) =>
        set((state) => ({
          user: { ...state.user, ...userNames },
        })),
    }),
    {
      name: "persist:user",
    },
  ),
);

export default useUserStore;
```

해당 에러를 해결하기 위해 useEffect로 isClient를 탐지하는 방식을 사용했습니다.

<br/>

### useHydratedStore

Next.js 공식문서에 나온대로 isClient flag를 컴포넌트마다 확인할 수도 있지만, 가독성도 떨어지고 비효율적이라는 생각이 들었습니다. 게다가 `React Hydration Error`는 Zustand Store를 가져다 사용하는 부분에만 발생했기에 관련 코드만 확인하면 될 일이었습니다. 따라서, 다음과 같이 `useHydratedStore`로 isClient시에만 `Zustand Store`를 가져올 수 있도록 처리했습니다.

<br/>

1.  인자로 zustand의 useStore, 해당 store의 초기값, selector를 받아
2.  useEffect로 초기 렌더링 이전이라면, SSR이므로 초기 store에서 selector로 필요한 값을 반환하고
3.  이후라면, CSR이므로 실제 store에서 selector로 필요한 값을 반환

```js
import { useEffect, useState } from "react";
import { StoreApi, UseBoundStore } from "zustand";

const useHydratedStore = <T, V>( //hydration 여부로 store를 select한 값을 반환 -SSR, CSR 미스매치 에러 해결
  useStore: UseBoundStore<StoreApi<T>>,
  initialStoreState: T
) => {
  const [isHydrated, setIsHydrated] = useState(false); //hydrated됐는지 여부이기에 isClient보다 isHydrated가 더 적합하다고 생각했습니다.
  const storeState = useStore((state) => state);

  useEffect(() => {
    setIsHydrated(true);
  }, []);

  if (isHydrated) {
    return storeState;
  }

  return initialStoreState; //만약 SSR이라면
};

export default useHydratedStore;
```

isHydrated되기 전, null 또는 undefined인 storeState을 반환할 수도 있지만 그런경우, 컴포넌트에서 null에 대한 예외처리를 해줘야 하는 불편함이 있어 아예 초기값을 만들어 줬습니다. 그리고 초기값은 해당 Zustand Store에서 관리하도록 처리했습니다.

```jsx
//useUserStore에 추가된 초기값
export const INITIAL_USER = {
  _id: "",
  ...생략,
};

export const INITIAL_USER_STORE_STATE = {
  user: INITIAL_USER,
  setUser: () => {},
  clearUser: () => {},
  updateUserBy: () => {},
};
```

페이지에서 사용시 다음과 같이 사용하면 됩니다. 페이지별로 isHydrated 플래그를 넣지 않아도 되고, useStore 초기값이 있기에 undefined 예외 처리를 따로 할 필요가 없습니다.

```jsx
export default function App() {
  const { user } = useHydratedStore(useUserStore, INITIAL_USER_STORE_STATE);

  return <h1>{user.name}</h1>;
}
```

만약 `useHydratedStore`로 관련 로직을 분리하지 않았다면 View와 관련없는 로직이 이만큼이나 늘어났을 겁니다. 😥

```jsx
export default function App() {
  const [isClient, setIsClient] = useState(false);
  const { user } = useUserStore((state) => state);

  useEffect(() => {
    setIsClient(true);
  }, []);

  return <h1>{isClient ? user.name : "no"}</h1>;
}
```

이걸 보고 `useHydratedStore`를 보니 속이 뻥 뚫리는 기분이네요...앞으로도 제 속을 위해 깔끔하고 직관적인 코드를 짜도록 노력해야 겠습니다.

<br/><br/><br/>

### 참고

[Next.js 공식문서](https://nextjs.org/docs/messages/react-hydration-error)
