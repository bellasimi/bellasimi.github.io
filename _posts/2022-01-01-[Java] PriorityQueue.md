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

저번에 [Queue 메소드](https://bellasimi.github.io/java/Java-Queue-Method/)에대해 알아봤는데요. 
오늘은 이어서 Queue에 우선순위를 부여하고 해당 순서에 따라 출력순서를 정해주는 PriorityQueue 클래스에 대해 알아보도록 하겠습니다. 
<br/>
<br/>
# 객체 생성

```
import java.util.PriorityQueue;

//int 오름차순 우선순위(낮은 수가 우선순위 높음)
PriorityQueue<Integer> pq = new PriorityQueue<>();

//int 내림차순 우선순위(높은 수가 우선순위 높음)
PriorityQueue<Integer> pq= new PriorityQueue<>(Collections.reverseOrder());

//String
PriorityQueue<String> pq= new PriorityQueue<>(); 

//String
PriorityQueue<String> pq= new PriorityQueue<>(Collections.reverseOrder());


```

PriorityQueue의 생성자 함수에 매개변수로 큐의 우선순위를 지정해줍니다. 

기본값은 오름차순으로 값이 커질수록 우선순위가 낮아집니다. 
만약 Collections.reverseOrder()로 내림차순 정렬을 해준다면 값이 작아질수록 우선순위가 낮아집니다. 

<br/>
# 주요 메소드 

| 메소드 | 기능 |
| :---: | :--- |
| **add(값)** | 큐에 값 추가, 성공여부에 따라 반환값 있음|
| **offer(값)** | 큐에 값 추가 |
| **poll()** | 우선순위 가장 높은 값 삭제, 큐가 빈값이면 null반환 |
| **remove()** | 우선순위 가장 높은 값 삭제|
| **remove(인덱스)** | 해당순위(인덱스)의 값 삭제|
| **clear()** | 큐 전체 비우기 |
| **peek()** | 우선 순위가 가장 높은 값 출력 |

<br/>

# 값 추가 

```
pq.add(1);
pq.offer(2);
```

둘다 값 추가 해주는 메소드지만 add는 삽입 성공시 true, 실패시 IllegalStateException 에러를 발생시킵니다. 
우선순위 큐에 값이 들어오면 그즉시 기존값과 비교해 해당값을 정렬합니다. 

<br/>
# 값 삭제

```
pq.remove();
pq.poll();
pq.remove(2);
pq.clear();

```

poll, remove 메소드를 사용하면 가장 우선순위가 높은 값을 삭제하고 clear메소드를 사용하면 큐전체를 삭제합니다.

❗ 단 remove함수의 경우 ❗

remove(2)처럼 매개변수에 값을 넣어주면, 해당 순위(인덱스)의 값을 지정해 삭제할 수 있습니다. 

<br/>
# 값 확인 

```
pq.peek();

//출력
System.out.println(pq);

//순회 : for문
for(int p: pq){
    System.out.println(p);
}

//순회 : iterator
Iterator<Integer> it = pq.iterator();
while(it.hasNext()){
    int pp = it.next();
    System.out.println(pp);
}

```


peek 메소드를 사용하면 우선순위가 가장 높은 값을 가져올 수 있습니다. 
만약 모든 요소를 순회하고 싶다면 for문이나 Iterator를 사용하도록 합시다.
<br/>
# 특징

* 내부 요소는 힙으로 구성됨, 이진 트리 구조로 이뤄져 있음

* 내부구조가 힙으로 구성 돼시간 복잡도는 O(NLogN)

* 입력 순서가 아닌 특정기준으로 출력하고 싶을 때 사용

* 객체 생성시 매개변수로 정렬기준을 받음(기본값은 오름차순)


<br/><br/><br/>


# 참고

💻 [시간복잡도](https://blog.chulgil.me/algorithm/)

💻 [PriorityQueue](https://coding-factory.tistory.com/603)

