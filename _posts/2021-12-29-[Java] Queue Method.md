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

# Queue 객체 생성

> Queue<Integer> que = new LinkedList<>();

제너릭 안에 자료형은 원하는 것으로 바꾸면 된다. 


# Queue 값 추가 

> que.add(1)
> que.offer(2)


## 1. add

* 값추가 성공시 true 반환

* queue 보다 큰 값 추가시 IllegalStateException 에러남

## 2. offer 

* 값 추가 성공시 true 반환

* 값 추가 실패시 false 반환


# Queue 값 삭제

## 1. remove() : 맨 위 값만 삭제, queue가 비었을 때 삭제하면 예외 발생

## 2. poll() : 맨 위 값만 삭제,queue가 비었을 때 삭제하면 null 반환

## 3. clear() : queue 전체 비우기



# Queue 값 확인 


> queue.peek()

맨 위값을 확인 


