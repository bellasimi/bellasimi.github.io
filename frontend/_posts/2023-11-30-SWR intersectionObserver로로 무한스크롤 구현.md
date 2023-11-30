---
title: "SWR intersectionObserver로 무한스크롤 구현"
categories:
  - intersectionObserver
  - SWR
toc: true
toc_sticky: true
---

기존엔 해당 페이지의 목록값만 보여주면 되는 형태였기 때문에, params.page의 값에 따라 변경된 데이터를 보여주도록했습니다. 그러다가 더보기와 무한스크롤 UI로 개선이 필요했는데 Redux로 전체값을 관리하고 다음 페이지를 로딩할 때마다 배열에 값을 추가하는 방식은 비효율적이란 생각이들었습니다.

마침 Redux를 SWR로 개선하는 작업중이었기에, SWR에서 인피니트로딩을 위해 제공하는 훅 `useSWRInfinite`를 사용해보기로 했습니다.

<br/>

기본적인 사용방법 다음과 같습니다.

```js
import useSWRInfinite from 'swr/infinite'

// ...
const { data, error, isLoading, isValidating, mutate, size, setSize } = useSWRInfinite(
  getKey, fetcher?, options?
)
```

**파라미터**

1. getKey: useSWR과 달리 useSWRInfinite는 getKey라는 함수로 요청에 대한 키를 받습니다. 이는 쿼리가 page변화를 감지해 key값을 바꿔주기 위함입니다.

   ```js
   const getKey = (pageIndex: number, previousPageData: any) => {
     if (previousPageData && !previousPageData.length) {
       return null;
     } // 끝에 도달한 경우

     return API_KEY + queryString({ ...params, page: pageIndex + 1 });
   };
   ```

2. fetcher: useSWR의 fetcher와 동일합니다. getKey의 반환값 key를 가지고 비동기 요청을 보내고 data를 반환합니다.
3. options: useSWR의 options에 다음과 같은 내용이 추가됐습니다.
   - initialSize = 1: 초기에 로드해야 하는 페이지의 수
   - revalidateAll = false: 항상 모든 페이지의 갱신 시도
   - revalidateFirstPage = true: 첫 번째 페이지를 항상 revalidate할 지 여부입니다. 기본값이 true이기 때문에 새로운 page의 데이터를 추가로 요청하는 중간중간 첫 번째 페이지를 다시 요청합니다. 만약 재검증이 굳이 필요하지 않다면 false로 둬도 됩니다.
   - persistSize = false: 첫 페이지의 키가 변경될 때, 페이지 크기를 1(initialSize가 설정된 경우 initialSize)로 초기화하지 않음
   - parallel = false: 여러 페이지를 병렬적으로 요청하는 옵션으로 true로 하는 경우 동시에 요청을 처리하기에 빠릅니다. 이경우 getKey의 previousPageData값이 항상 null이라 끝에 도달한 경우 아무것도 반환하지 않는 조건문은 동작하지 않습니다.

<br/>

**반환값**

1. data: 각 페이지의 응답 값의 배열.
2. error: useSWR의 error와 동일
3. isLoading: useSWR의 isLoading과 동일
4. isValidating: useSWR의 isValidating과 동일
5. mutate: useSWR의 바인딩 된 뮤테이트 함수와 동일하지만 데이터 배열을 다룸
6. size: 가져올 페이지 및 반환될 페이지의 수
7. setSize: 가져와야 하는 페이지의 수를 설정하는 함수입니다. 스크롤을 내리면 다음과 같이 setSize를 호출해 기존값에 +1를 그러면, getKey의 pageIndex가 +1되면서 다음 페이지를 요청하는 식입니다.
   ```js
   const handleLoadMore = () => {
     if (!isLoading && !isReachingEnd) {
       setSize((prev) => prev + 1);
     }
   };
   ```

<br/>

### useSWRInfinite 자세한 코드 예시

이제부터는 해당 훅을 어떻게 사용하면 좋을 지 실제 코드를 보면서 설명하도록 하겠습니다.

<br/>

먼저 useSWRInfinite를 필요한 값들과 함께 훅으로 모듈화해줍니다. examination 목록을 무한스크롤로 가져오는 훅을 만들 것이기 때문에, 훅의 이름을 `useGetInfiniteExaminations`라고 지어줬습니다. 이렇게 하는 이유는 useSWRInfinite에 관련된 비즈니스 로직을 분리해 가독성을 높이고 유지보수를 용이하게 만들기 위합입니다. (특정 요청마다 key, fetcher의 형태가 정해져 있기에 가능합니다.) 전체 코드는 다음과 같습니다.

<br/>

- useGetInfiniteExaminations.tsx : examination 목록 조회 무한스크롤

```jsx
export const useGetInfiniteExaminations = ({
  companyId,
  procedureId,
  options,
}: {
  companyId: string;
  procedureId?: string;
  options?: any;
}) => {
  const API_KEY = `/api/v1/participants?companyId=${companyId}&procedureId=${procedureId}&`;
  const { params } = useSelector((state: RootState) => state.participants);
  const { t } = useLocalization();

  const getExaminations = async (url: string) => {
    try {
      const { data } = await axiosInstance.get(url);
      return data.examinations;
    } catch (error: any) {
      if (error?.response.message) {
        Toast.show(t(error.response.message), ToastType.Fail);
        return;
      }
    }
  };

  const getKey = (pageIndex: number, previousPageData: any) => {
    if (previousPageData && !previousPageData.length) {
      return null;
    } // 끝에 도달한 경우

    return API_KEY + queryString({ ...params, page: pageIndex + 1 });
  };

  const { data, mutate, error, isLoading, setSize, size } = useSWRInfinite<
    Examination[]
  >(getKey, procedureId ? getExaminations : null, options && { ...options });

  const PAGE_SIZE = 10;
  const examinations = data ? data.flat() : [];
  const isLoadingMore =
    isLoading || (size > 0 && data && typeof data[size - 1] === "undefined");
  const isEmpty = data?.[0]?.length === 0;
  const isReachingEnd =
    isEmpty || (data && data[data.length - 1]?.length < PAGE_SIZE);

  return {
    data: examinations,
    mutate,
    error,
    isLoading: isLoadingMore,
    isReachingEnd,
    setSize,
    size,
  };
};

```

여기서 눈여겨 볼 부분은 useSWRInfinite 아래 값들입니다. 해당 값들은 필요하지만, useSWRInfinite로 바로 반환되지 않기에 직접 구해야 합니다.

1. PAGE_SIZE: 페이지별로 몇 개의 데이터가 들어 있는지를 나타냅니다.
2. examinations = data ? data.flat() : [];
   - data는 page별 examinations배열을 가진 이중배열입니다.([[page1의 examinations],[page2''],...])
   - 그러므로 전체 examinations를 얻으려면 flat해야 합니다.
3. const isLoadingMore =
   isLoading || (size > 0 && data && typeof data[size - 1] === "undefined");
   - size가 0보다 크고, data가 있고, data[size-1]이 undefined일 때 역시 로딩중이라고 판단합니다.
4. const isEmpty = data?.[0]?.length === 0;
   - data가 비어있거나, data의 마지막 요소의 길이가 PAGE_SIZE보다 작을 때 더 이상 로드할 데이터가 없다고 판단합니다.
5. const isReachingEnd =
   isEmpty || (data && data[data.length - 1]?.length < PAGE_SIZE);
   - getKey로 끝에 도달한 경우 api 호출을 막지만, intersectionObserver의 콜백으로 getKey가 여러번 호출될 수 있기에 해당 값으로 콜백을 더 이상 호출하지 않도록 해줍니다.

<br/>

### page 1 에서 전체 examination 수를 알아야 한다면?

useSWRInfinite역시 스크롤이 있는 page까지만 examinations를 가져오기에 반환된 data.length로는 전체 값을 알 수 없습니다. 따라서 서버에서 해당값을 보내줘야 합니다. 저희팀 역시 서버에서 요청시 totalCount라는 필드로 해당 값을 전해주고 있었는데요. 이경우 `useGetInfiniteExaminations`에서 다음과 같은 수정이 필요합니다.

```js
export const useGetInfiniteExaminations = ({
  companyId,
  params,
  options,
}: Props) => {
  //동일한 부분은 생략
  const getExaminations = async (url: string) => {
    try {
      const { data } = await axiosInstance.get(url);

      return data; //data.examination만 가져오던 전과 달리 totalCount까지 전부 가져옴
    }
  };

  const { data, mutate, error, isLoading, setSize, size } = useSWRInfinite<{
    examinations: Examination[];
    totalCount: number; // getExaminations의 반환값에 따라 타입 수정
  }>(getKey, getExaminations, options && { ...options });

  const totalCount = data ? data[0]?.totalCount : 0; // 페이지와 상관없이 totalCount값은 일정하기에 첫번째 데이터의 totalCount값을 사용
  const examinations = data
    ? data.map((item) => item && item.examinations).flat()
    : []; //data에서 examinations 배열만 뽑아 이중배열로 만들고 flat해서 전체 examination를 구한다.

  //빈값인지 마지막 페이지인지 알기 위해서 data가 아닌 data의 examination를 확인한다.
  const isEmpty = data?.[0]?.examinations.length === 0;
  const isReachingEnd =
    isEmpty || (data && data[data.length - 1]?.examinations.length < PAGE_SIZE);

  return {
    data: examinations,
    totalCount,
    //동일한 부분은 생략
  };
};
```

### intersectionObserver로 스크롤 감지하기

onScroll로 setSize를 하면 스크롤이 하단에 닿지 않아 여전히 같은 페이지임에도 다음 페이지 요청을 보냅니다. 페이지 높이를 계산한다고 해도 굉장히 비용이 많이 들기에 viewport 아래까지 스크롤을 내렸는지 감지하고 callback를 호출해주는 intersectionObserver를 사용했습니다. `intersectionObserver` 역시 관련된 코드와 함께 `useGetInfiniteExaminations`라는 훅으로 모듈화 해줍니다.

**useIntersectionObserver.tsx intersectionObserver를 관리하는 훅**

```jsx
/**
 *
 * @param onIntersection intersection 발생시 실행할 함수
 * @param options IntersectionObserver 옵션
 * @returns ref intersection을 감지할 참조 대상 엘리먼트
 */

export const useIntersectionObserver = (
  onIntersection,
  options: IntersectionObserverInit = { threshold: 0.0 }
) => {
  const ref = useRef(null);

  const callback = useCallback(
    (entries) => {
      entries.forEach((entry) => {
        //상위 요소와 ref요소 교차할 때 onIntersection 실행
        if (entry.isIntersecting) {
          onIntersection();
        }
      });
    },
    [onIntersection]
  );

  useEffect(() => {
    if (!ref.current) {
      return;
    }

    const observer = new IntersectionObserver(callback, options);
    observer.observe(ref.current);

    return () => {
      observer.disconnect();
    };
  }, [callback, ref, onIntersection, options]);

  return ref;
};
```

반환값 useRef가 요소를 참조하고, intersectionObserver가 해당 요소를 관찰합니다. 그러다가 `entry.isIntersecting` 상위요소와 교차하면 (스크롤이 하단까지 내려가면) `onIntersection`을 실행합니다.

<br/>

### 사용얘시: useSWRInfinite & useIntersectionObserver

examination 목록을 보여주는 페이지는 다음과 같은 구조입니다.

```jsx
<ErrorBoundary fallback={<Error />}>
  <Suspense fallback={<Loading />}>
    <LoadMoreObserver>
      <ExaminationList />
    </LoadMoreObserver>
  </Suspense>
</ErrorBoundary>
```

`ExaminationList` 컴포넌트에서 목록을 그리고, `LoadMoreObserver`컴포넌트에선 무한스크롤관련된 로직을 처리합니다. `LoadMoreObserver`를 자세히 보면 children 아래 div를 두고 있습니다. 이 div가 바로 `useIntersectionObserver`의 ref로 페이지에 드러났는지 감지할 요소입니다. 첫 페이지에선 `ExaminationList`가 없기에 해당 요소가 감지되서 요청을 바로 보냅니다. 하지만 `ExaminationList`를 가져온 요소가 화면 밖에 있기에 스크롤을 맨 아래로 내리기 전까진 요청을 보내지 않습니다.

```jsx
const ExaminationsFetcher = ({ children }: Props) => {
  const dispatch: AppDispatch = useDispatch();
  const { procedureId } = useParams();
  const { _id: companyId } = useSelector(
    (state: RootState) => state.sessions.company
  );

  useEffect(() => {
    dispatch(paramsReset());
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);

  const { error, setSize, mutate, isLoading, isReachingEnd } =
    useGetInfiniteExaminations({
      companyId,
      procedureId,
    });

  //useIntersectionObserver에서 onObserver시 호출할 함수
  const handleLoadMore = () => {
    if (!isLoading && !isReachingEnd) {
      //만약 로딩중, 마지막페이지라면 useGetInfiniteExaminations에서 아무 호출도 일어나지 않는다.
      setSize((prev) => prev + 1);
    }
  };

  //useIntersectionObserver 반환 값 => intersection여부를 탐지할 대상
  const intersectionTarget = useIntersectionObserver(handleLoadMore);

  //...생략
  return (
    <>
      {children}
      <div ref={intersectionTarget} /> //해당 요소가 viewport에 드러나는 순간 그
      다음 페이지까지 데이터를 가지고 옴
    </>
  );
};
```

<br/><br/><br/>

### 참고

[인피니트 로딩 – SWR](https://swr.vercel.app/ko/examples/infinite-loading)
