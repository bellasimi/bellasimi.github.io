---
title: "[ALGORITHM] 시간복잡도와 정렬"
categories:
  - algorithm
tags:
  - js
  - 시간복잡도
  - 정렬
toc: true
toc_sticky: true
---

![js](https://user-images.githubusercontent.com/79133602/159547044-d4425e2f-1a97-487f-9855-cceb721f6bce.png)

<br/>

# 시간 복잡도

> 프로그램의 성능 측정

프로그램이 돌아가기만 하면 끝일까?

어떤 자료 구조로 어떻게 코딩하는 가에 따라 걸리는 시간이 다르다. 당연히 빠른 놈이 성능이 좋으니까 신경 써야겠지.

<br/>

## 측정 방법 - 자바스크립트

```
const start = new Date.getTime();

//시간복잡도를 측정할 코드 여기에 작성

const end = new Date.getTime();

console.log(end-start); //얼마 걸렸나 계산

```

<br/><br/>

# Big O 표기법

> 시간 복잡도 표기법

![image](https://user-images.githubusercontent.com/79133602/160537714-481969ac-1676-4950-a7c5-f83af51889a6.png)

## 예시

O(n) 선형 시간 : 배열의 경우 값 하나 삭제하면 입력값 갯수만큼 자리이동을 함

O(C) 상수 시간 : 큐의 경우 앞의 값이 삭제되도 인덱스가 밀리지 않고 앞의 인덱스가 다음 인덱스로 바뀜. 1개만 바뀌는 상수시간

```
for(let i = 0; i< n; i++ ){
 //조건문 n이 어떤 상태인지에 따라 시간복잡도 달라짐
 // 상수< log< 선형:input < 선형 log < 다중루프 < 지수 < n!
}
```

<br/>

## 법칙

- 계수 법칙: n이 무한에 가까울 수록 n에 곱하는 상수의 크기는 의미가 없다.

- 합의 법칙: 루프가 따로 있는 경우

- 곱의 법칙: 다중 루프

- 다항 법칙 : n과 n^의 시간복잡도 차이는 n^만큼 늘어남

<br/><br/><br/>

# sort()

> arr.sort((a,b) => {return a와 b의 연산 })

a의 자리구하기 : 자리는 -면 앞자리 0이면 현재자리 +면 뒷자리

    a: 현재값
    b: 비교대상

## 내림차순

> arr.sort((a,b) => b-a )

a가 비교대상 보다 크면 앞자리 -, 작으면 뒷자리+

    1. b-a>0 == b>a a가 작으면 자리 0+
    2. b-a<0 == b<a  a가 크면 자리 0-
    3. b-a == 0 같으면 자리는 그대로 0

## 오름차순

> arr.sort((a,b) => a-b )

a가 비교대상 보다 작으면 앞자리 - , 크면 뒷자리 +

    1. a-b<0 == a<b a가 작으면 자리 0-
    2. a-b>0 == a>b a가 크면 자리  0+
    3. a-b == 0 같으면 자리는 그대로 0

<br/>
<br/>
<br/>

# 느낀점

평소 시간 복잡도를 계산하긴 했지만 문제를 풀기전 예측을 해본 적은 없다. 또 빅오 표기법으로 나타내는 법도 잘 몰랐다.

코딩테스트를 잘 보기 위해선 어떤 자료구조를 써야 되는지 미리 알아야 되는데 이때 자료 구조 마다 빅오 표기가 어떻게 되는지 시간복잡도를 알아야 된다는 걸 알았다.

<br/>

> 입출력 제한으로 자료구조 파악

입력이 100 이하

- 완전 탐색
- 백트래킹

10,000 이하

- 최대 O(n^2) 이내로 풀기

1,000,000 이하

- 최대 O(n log n) 이내로 풀기
- 힙, 우선 순위 큐
- 정렬
- 동적 계획 법
- 최단거리

천만이상

- 최대 선형
- 루프한번
- 동적 계획법
- 그리디

<br/><br/><br/><br/>

# 참고

💻 [프로그래머스 스쿨](https://programmers.co.kr/?utm_source=google&utm_medium=cpc&utm_campaign=brand_prgms_pc&gclid=CjwKCAjwuYWSBhByEiwAKd_n_u7a0X7xZqts4x1EH2x0MWOGqVMQiyD5AgCVZxAv_P9fLGAjQLhaExoCl8IQAvD_BwE)

💻 [이선협 강사님 특강](https://github.com/kciter)
