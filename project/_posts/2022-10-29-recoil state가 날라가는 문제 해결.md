---
title: "[맛이어때] recoil state가 날라가는 문제 해결"
categories:
  - project
tags:
  - 맛이 어때
toc: true
toc_sticky: true
---

![image](https://user-images.githubusercontent.com/79133602/199004774-b72f1d26-f4e7-438e-9874-323c2f11c33f.png)

## 문제

Atom으로 사용자 정보를 관리하는데 따로 값을 저장하지 않기에 새로고침 시 값이 날라가는 문제가 있었습니다.

![video](https://user-images.githubusercontent.com/79133602/199007974-2ff26ba5-db5b-4983-90c2-dcd3b957c298.mp4)

<br/>

## 고민

Atom effect, recoil-persist를 사용하면 localStorage에 atom을 저장, 새로고침에도 날라가지 않지만 해당 부분은 SSR에 적합하지 않았습니다.

<br/>

## 해결

따라서 사용자 정보를 `react-cookie`를 사용해, 서버에서도 접근 가능한 쿠키에 저장하고, Atom effect 코드를 쿠키에 맞도록 수정해서 문제를 해결했습니다.

```jsx
import { atom } from 'recoil'
import { User } from '@interfaces'
import { v1 } from 'uuid'
import { DEFAULT_USER_IMAGE } from '@constants/image'
import { setCookie, getCookie } from '@utils/cookie'
import { TOKEN_EXPIRE_DATE, CURRENT_USER } from '@constants/token'

export const initialUser = {
  id: null,
  image: DEFAULT_USER_IMAGE,
  email: '',
  nickName: '',
  snsAccount: '',
  createdAt: '',
  menuCount: 0
}

interface Props {
  setSelf(userValue: User | null): void
  onSet(newValue: User, _: any, isReset: boolean):void
}

const cookieEffect =
  (key: string) =>
  ({ setSelf, onSet }: Props) => {
    const savedValue = getCookie(key)

    if (savedValue != null) {
      setSelf(savedValue || initialUser)
    }

    onSet((newValue: User, _: any, isReset: boolean) => {
      const expirationDate = getCookie(TOKEN_EXPIRE_DATE)
      isReset
        ? setCookie(key, '')
        : setCookie(key, JSON.stringify(newValue), {
            path: '/',
            expires: new Date(expirationDate)
          })
    })
  }

export const currentUser = atom<User>({
  key: `currentUser/${v1()}`,
  default: initialUser,
  effects: [makeCookieEffect(CURRENT_USER)]
})
```

<br/><br/><br/>

## 참고

[Recoil로 전역 상태 관리하기](https://velog.io/@chchaeun/Recoil%EB%A1%9C-%EC%A0%84%EC%97%AD-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0)
