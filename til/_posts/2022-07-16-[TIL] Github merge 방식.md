---
title: "[TIL] Github merge 방식"
categories:
  - til
tags:
  - til
  - github
toc: true
toc_sticky: true
---

![image](https://user-images.githubusercontent.com/79133602/161557696-fe3b688d-f6d2-4073-a18f-8d57377acaa7.png)

<br/>

## 1. non fast-forward

> 빨리감기를 할 수 없다

항상 해당 에러를 만날 때마다 막연히 기존 base가 달라져서 충돌하고 있구나 정도로만 생각했지 빨리 감기를 할 수 없다는 게 무슨 의미인지는 고민하지 않았다. 그래서 오늘 다시 공부해봤다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c51ef3f1-99c2-4147-b5e9-71469e95c7b1/Untitled.png)

위 이미지를 보면 feature2의 경우 빨리감기가 가능하다

<br/>

> **빨리감기란?**

- develop : a-b-c
- feature2: a-b-c-d

feature2를 develop에 merge할 때 `a-b-c` + `a-b-c-d` = `a-b-c-a-b-c-d` 가 아니라 곂치는 `a-b-c`
에서 바로 `-d`로 이동하는 걸 빨리감기라고 한다.

<br/>

> **빨리감기가 안되는 경우**

merge될 branch의 값이 base와 달라져서서 안된다. feature1은 `a-b-c` 만 갖고 있는데 갑자기 `d`
가 끼어 들어서 이 땐 중복 커밋을 생략하고 새로운 커밋만 붙이는 fast-forward를 할 수없다.

<br/>

> **3way- merge**

그럼 이 땐 바뀐 부분까지 포함해서 merge를 고려하면 된다. 그러기 위해 새로운 d를 feature1으로 가져온다. rebase, squash, 일반 선택해서 merge한다.

<br/><br/>

## 2. merge의 종류

github pr의 merge pull request를 보면 다음과 같이 3종류의 merge가 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/696edf0b-e26b-4f6c-aea9-a99006d6209f/Untitled.png)

<br/>

### create a merge commit

기존에 우리가 하던 일반적인 merge다. 기능 브랜치는 merge하려는 develop에서 따로 확인이 가능하고 커밋 내역도 전부 존재한다.

- 장점
  - 버그 발생 시 추적이 상대적으로 쉽다.
  - commit history에 들어가서 추적한 파일의 원본을 볼 수 있다.
- 단점
  - 브랜치가 여러개면 merge 내역을 알아보기 힘들다.
  - commit history가 지저분 하다.

<br/>

### squash and merge

전체 commit들이 merge commit 하나로 합쳐진 뒤 develop의 base에 붙인다.

- 장점
  - commit history가 깔끔하다.
  - rebase와 달리 merge된 브랜치의 작업 시점을 파악할 수 있다.
- 단점
  - 버그 발생시 추적이 힘들다.

<br/>

### rebase and merge

전체 commit들이 develop 뒤에 바로 이어지고 commit의 번호도 바뀐다.

- 장점
  - 깔끔한 history
  - commit 내역도 확인 가능 (버그 추적 가능)
- 단점
  - base를 merge하려는 브랜치 맨뒤로 하기에 작업시점을 파악하기 힘들다.
  - commit 번호가 바뀌기 때문에 중간에 떼서 작업한 내역이 있다면 충돌한다.
