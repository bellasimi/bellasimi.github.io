---
title: 
sidevar:
  nav: "docs"
categories:
- java
tags:
- java
- queue
last_modified_at:
---


Queue는 Stack의 LIFO(LastInFirstOut) 선입후출 방식과 반대로 FIFO(FirstInFisrtOut) 선입선출 방식을 따릅니다. 

아래와 같은 메소드를 사용해 Queue를 조작할 수 있습니다.  

<br/>
# Queue 객체 생성

> Queue<Integer> que = new LinkedList<>();

제너릭 안에 자료형은 원하는 것으로 바꾸면 됩니다.

<br/>

# Queue 값 추가 

> que.add(1)
> que.offer(2)

## 1. add

* 값추가 성공시 true 반환

* queue 보다 큰 값 추가시 IllegalStateException 에러남

## 2. offer 

* 값 추가 성공시 true 반환

* 값 추가 실패시 false 반환

<br/>

# Queue 값 삭제

## 1. remove() 

맨 위 값만 삭제, queue가 비었을 때 삭제하면 예외 발생

## 2. poll() 

맨 위 값만 삭제,queue가 비었을 때 삭제하면 null 반환

## 3. clear() 

queue 전체 비우기


<br/>

# Queue 값 확인 

> queue.peek()

맨 위값을 확인 

<br/>
# 순서 지정

만약 입력된 순서가 아니라 사용자가 지정한 우선순위로 데이터를 출력하고 싶다면 PriorityQueue를 사용하면 됩니다. 

[PriorityQueue 사용법](https://bellasimi.github.io/java/Java-PriorityQueue/)


