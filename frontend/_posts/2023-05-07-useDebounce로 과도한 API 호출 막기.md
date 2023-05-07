---
title: "useDebounce로 과도한 API 호출 막기"
categories:
  - debounce
toc: true
toc_sticky: true
---

### debounce란

전에 debounce 기법에 대해 설명한 적이 있었는데요. ([관련글](https://bellasimi.github.io/cs/CS-Debounce-&-Throttle/)) onChange시 쓸데없는 API 호출을 방지하는 기능을 합니다. 바닐라 자바스크립로 debounce를 구현할 때는 다음과 같이 onChange가 발생하는 요소에 직접 addEventListener로 keyup 이벤트가 발생 할 때 의미없는 키워드로 검색을 하지 않도록 일정시간 지연을 했는데요. 해당 기능을 리액트에서 구현하려면 어떻게 해야 할까요?

```js
textarea.addEventListener("keyup", async (e) => {
  let timer;

  if (timer) {
    clearTimeout(timer);
  }

  timer = setTimeout(
    postApi({
      content: e.target.value,
    }),
    일정시간
  );
});
```

<br/>

### 리액트에서 debounce 구현하기

자바스크립트에선 이벤트를 처리할 때 인라인이 아니라, addEventListener를 사용하라고 합니다. 그래야 한 컴포넌트에 여러 핸들러를 붙일 때, 메모리 관리를 할 때 편리하기 때문입니다. 하지만, 리액트에선 이와 반대로 addEventListener 보다 요소에 인라인으로 제공하기를 권장합니다. 리액트(17버전 이상)는 ROOT ELEMENT에 이벤트 리스너를 붙여 사용하는데 이럴 경우 굳이 addEventListener를 사용하지 않아도 관리가 가능합니다. 따라서 다음과 같이 직접 textArea에 이벤트 핸들러를 붙여줍니다.

```jsx
export default function Component () {

  return <textarea onChange={이벤트 핸들러}/>
}
```

이제 onChange시 postApi 호출을 지연하도록 debounce를 구현하도록 해보겠습니다.

```jsx
export default function Component() {
  const handleKeywordChange = async (e) => {
    let timer;

    if (timer) {
      clearTimeout(timer);
    }

    timer = setTimeout(
      postApi({
        content: e.target.value,
      }),
      일정시간
    );
  };

  return <textarea onChange={keywordChangeHandler} />;
}
```

위와 같은 방식으로 구현가능하지만, 재사용성이 떨어지고, keyword값을 state로 갖고 있을 수 없다는 단점이 있습니다.

<br/>

### 좀 더 리액트다운 방식으로 개선하기

그래서 다음과 같이 useDebounce라는 커스텀 훅을 만들어봤습니다. 첫번째 인자로는 api호출을 담당하는 callback 함수를, 두번째 인자로는 setTimeout으로 지연시킬 시간을, 3번째로는 onChange 변화를 감지할 의존배열을 받습니다.

```jsx
import { useEffect, useRef } from "react";

const useDebounce = (
  callback: () => void,
  delay: number,
  dependencies: string[]
) => {
  const timerRef = useRef<NodeJS.Timeout>();

  useEffect(() => {
    if (timerRef.current) {
      clearTimeout(timerRef.current);
    }
    const handler = setTimeout(callback, delay);
    timerRef.current = handler;

    return () => {
      clearTimeout(timerRef.current);
    };
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [callback, delay, timerRef, ...dependencies]);

  return;
};

export default useDebounce;
```

그리고 사용할 때는 다음과 같이 useEffect를 연상케하는 형태로 특정값이 변할 때 debounce가 0.3초 간격으로 작동함을 직관적으로 알 수 있습니다.

```jsx
export default function Component() {
  const [keyword, setKeyword] = useState("");

  useDebounce(
    () => {
      postApi({ content: keyword });
    },
    300,
    [keyword]
  );

  return (
    <textarea
      onChange={(e) => {
        setKeyword(e.target.value);
      }}
    />
  );
}
```

<br/>

### 주의

useEffect로 만든 코드라.. 부수효과로 인한 오작동이 있을 수 있습니다. 예로, 검색어로 목록을 필터링 할 때 2페이지를 눌렀는데 계속해서 1페이지로 이동하는 문제가 있었습니다. 해당 에러의 원인은 다음과 같았습니다.

1. useDebounce 훅이 useEffect를 사용하기에 마운트되는 시점에 한번 실행됨
2. 따라서, 2페이지로 렌더링 됐을 때 useDebounce훅이 작동해서 `dispatch(paramsSet({ keywordTitle })` 가 실행되는데, 이로 인해 page값이 1로 변경된 상태로 리렌더링하기 때문

<br/>

### 1차 해결 과정

- 1페이지로 안가게 하면 되지 않아? 안돼!

  - paramsSet action은 필터링을 위한 것, 필터링한 이후 데이터의 첫번 째 페이지로 보여주는 게 당연하기에 page가 1로 변하는 것은 당연했습니다.

    ```jsx
    paramsSet(
          state,
          action: PayloadAction<{
            keywordTitle?: string;
            sort?: string;
            order?: number;
            status?: ProcedureStatus;
            page?: number;
            size?: number;
          }>
        ) {
          // iterate through the payload object and set the state

          //새로 필터링할 때 첫 패이지로
          const params = { ...state.params, page: 1 };

          const payload = action.payload;
          Object.keys(payload).forEach((key) => {
            const value = payload[key as keyof typeof payload];
            if (value !== undefined) {
              // @ts-ignore
              params[key] = value;
            }
          });

          state.params = params;
        },
    ```

- **해결: 그럼 마운트된 시점에는 useDebounce가 작동하지 않게 하면 어때?**
  최종적으로 다음과 같이 initialized state를 추가하고 렌더링, 리렌더링으로 마운트된 시점엔 해당 값이 false, onChange가 발생한 시점엔 true로 바꿔서 useDebounce가 검색이 발생한 경우만 작동되도록 했습니다.
  ```jsx
  useDebounce(
    () => {
      if (initialized) {
        dispatch(paramsSet({ keywordTitle }));
      }
    },
    300,
    [keywordTitle]
  );
  ```

<br/><br/><br/>

### 참고

[리액트 공식문서: 이벤트 처리](https://ko.legacy.reactjs.org/docs/handling-events.html)

[Web: React의 Event 시스템 내부 구현 자세히 알아보기 (React v18.2.0)](https://medium.com/hcleedev/web-react%EC%9D%98-event-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%82%B4%EB%B6%80-%EA%B5%AC%ED%98%84-%EC%9E%90%EC%84%B8%ED%9E%88-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-react-v18-2-0-39d59ab45bec)
