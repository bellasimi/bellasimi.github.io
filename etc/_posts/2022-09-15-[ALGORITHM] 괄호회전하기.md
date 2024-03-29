---
title: "[ALGORITHM] 괄호회전하기"
categories:
  - algorithm
tags:
  - algorithm
toc: true
toc_sticky: true
---

![image](https://user-images.githubusercontent.com/79133602/190297564-04af658a-83ee-4342-88b7-807d4f260fe4.png)

<br/>

# 풀이 과정

## 처음 풀이

> 오답: 정확도 21점

> 완전 탐색이라고 생각

처음엔 정규표현식을 사용해서 `const regex = /()|{}|[]/` 가 존재한다면 `replace(regext,'')`를 반복적으로 한뒤 남은 string 존재 여부로 answer++ 하려고 했다. 하지만 이미 괄호들은 정규표현식에 지정된 의미가 있기에 `/a|b|c/`같은 문자처럼 인식을 못해서 해당 방식은 사용할 수 없었다.

대신 올바른 문자를 배열로 두고 includes()를 사용해 소거하는 방식을 썼다.

하지만 정확성 테스트에서 21점... 을 받아 통과하지 못 했다.

```js
function solution(s) {
  let answer = 0;
  const length = s.length;
  for (let i = 0; i < length; i++) {
    const string = s.slice(i, length) + s.slice(0, i);
    if (findWrongString(string) === 0) answer++;
  }

  function findWrongString(string) {
    const correctArray = ["()", "{}", "[]"];
    while (true) {
      for (let correct of correctArray) {
        if (string.includes(correct)) {
          string = string.replace(correct, "");
          continue;
        }
        return string.length;
      }
    }
  }
  return answer;
}
```

## 오답 정리

> 틀린이유: correctArray를 반복해서 돌지 않았기 때문

regex를 쓸 때와 달리 correctArray를 돌리면 같은 값을 여러번 체크할 수 없다. 예를 들어 `(())`에서 `()`제거 후 continue를 하면 `['()','{}','[]']` 모든 배열값이 아니라 `()` 다음 배열 값만 체크를 한다.

따라서 `()`는 `['{}','[]']`가 있는지만 판단하기에 소거될 수 있음에도 string.length가 2가 되서 answer에 포함되지 못 한다.

## 해결

이를 해결하기 위해 한번 replace된 string은 break를 줘서 처음부터 correctArray를 돌려 includes 여부를 판단하기로 했다.

또 `checked` 변수를 만들어서 모든 correctArray를 돌았는데도 일치값이 없는지 판단할 수 있게 했다.

correctArray에서 돌면서 일치값이 있으면 `checked`를 초기화하고 일치되지 않는 경우 `checked` 변수에 1을 더한다. 모두 돌았는데도 소거 대상이 없다면 `checked===3`이 되므로 이 때 `return string.length`로 while문을 빠져나가도록 처리한다.

```js
function solution(s) {
  let answer = 0;
  const length = s.length;
  for (let i = 0; i < length; i++) {
    const string = s.slice(i, length) + s.slice(0, i);
    if (findWrongString(string) === 0) answer++;
  }

  function findWrongString(string) {
    const correctArray = ["()", "{}", "[]"];
    let checked = 0;
    while (true) {
      if (checked === 3) {
        return string.length;
      }
      for (let correct of correctArray) {
        if (string.includes(correct)) {
          string = string.replace(correct, "");
          checked = 0;
          break;
        }
        checked++;
      }
    }
  }
  return answer;
}
```

## 다른 사람의 풀이

> stack을 사용

> 시간 복잡도가 훤씬 낮아

먼저, 홀수는 올바른 괄호가 될 수 없기에 처음부터 답에서 제외한다.`if (s.length % 2 === 1) return 0;`

그리고 선입후출 구조인 stack을 사용해 반복되는 열림기호가 있다면 가장 내부의 열림 `(,{,[` 괄호부터 올바르게 닫히는 지 판단하는 게 핵심이다.

`flag`변수를 사용해서 1이면 올바르게 닫힌 거고, 0이면 아니다.

회전된 괄호 문자 string을 돌면서 각 char가 열림기호면 stack에 추가한다.
닫힘 괄호면 stack.pop한 char와 현재 char가 올바른 짝인지 비교하고 아니라면 `flag=0`으로 만든 뒤 break로 string 반복문을 빠져나온다. 만약 맞다면 반복문이 끝날 때까지 flag는 1이다.

반복문을 빠져나온 뒤 `if (flag) answer++;`조건문으로 올바르게 닫힌 경우엔 answer에 1을 더한다.

그리고 `for (let i = 0; i < sLen; i++)`가 남아 있다면 다음 반복문을 진행한다.

```js
function solution(s) {
  if (s.length % 2 === 1) return 0;
  const sLen = s.length;
  let answer = 0;

  for (let i = 0; i < sLen; i++) {
    let string = s.slice(i) + s.slice(0, i);
    const stack = [];
    let flag = 1;
    for (let char of string) {
      if (char === "(" || char === "{" || char === "[") stack.push(char);
      else {
        const last = stack.pop();
        if (char === ")" && last === "(") continue;
        if (char === "}" && last === "{") continue;
        if (char === "]" && last === "[") continue;
        flag = 0;
        break;
      }
    }
    if (flag) answer++;
  }
  return answer;
}
```

## 결론

스택으로 푸는 게 더 효율적이고 간단하다.

<br/><br/><br/>

# 참고

💻 [프로그래머스](https://school.programmers.co.kr/learn/courses/30/lessons/76502)
