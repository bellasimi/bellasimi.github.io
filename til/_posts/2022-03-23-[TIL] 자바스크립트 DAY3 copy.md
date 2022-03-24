---
title: "[TIL] 자바스크립트 DAY3"
categories:
- til
tags:
- til
- day3
---

![js](https://user-images.githubusercontent.com/79133602/159547044-d4425e2f-1a97-487f-9855-cceb721f6bce.png)

<br/>
<br/>

# 자료 구조 

> 큐, 스택, 트리,그래프

일대 일 연결관계인 선형 구조, 다대 다 연결관계인 비선형 구조가 있다. 오늘은 선형구조만 알아보자 

**자료구조 활용 예 )** 

- 검색, 자동완성 : TREE

- 줄서기 :QUEUE

- 좌석선택 테이블 : HASH TABLE

<br/>

# 선형 자료구조

> Array, LInked List, Stack, queue

한 원소뒤에 하나의 원소만이 존재, 자료들이 선형으로 나열돼 있다.

<br/>

## 1. 배열: 순차리스트

> 숫자 인덱스에 값을 저장

추가, 삭제가 많으면 적합하지 않아.. 인덱스를 옮기는 게 비효율 적이야... 
선형 시간이 소요된다구 😰

인덱스를  아는 경우: 검색에 유리! 

모르는 경우: 배열을 전부 순회;;

<br/>


## 자바스크립트 배열 특이점

> 동적이고 인덱스가 숫자가 아니어도 됨

```
const arr = [1,2];
arr.push(3); // 동적으로 값 추가
arr.pop(); //삭제
arr['name'] = 'shin' //HashMap 처럼 사용 가능 but 길이엔 영향 x 
console.log(arr);

```
자바스크립트의 배열이 근본적으로 객체 타입이기 때문에 이런 특이점이 있다. 인덱스에 숫자 말고 다른 자료형을 넣으면 배열의 길이에 계산되지 않는다.

<br/>

### 💡 활용

배열을 이용해 Queue, Linked List, Stack 등을 구현할 수 있다. class 객체로 만들어서 라이브러리처럼 사용하면 편하다.

<br/><br/><br/>

## 2.  연결 리스트

>  **데이터** + <span style="color:red">포인터</span> == **노드** 

각 요소(노드)를 포인터로 연결관리,
데이터 영역엔 값 + 포인터 영역엔 다음 노드가 들어 있음

추가, 삭제가 반복되면 얘가 좋지. 상수시간만 소요된다구 !
탐색은 선형시간


<br/><br/>

## 🤔 배열과 차이

- 메모리 차이 : 메모리 연속적으로 차지하는 배열과 달리, 퍼져있음 그래서 참조를 위해 포인터를 참조

- 삭제,추가 방식 : 삭제할 요소 선택 후 포인터를 통해 이전노드의 포인터를 다음 노드의 포인터에 연결 -> 상수 시간 소요

<br/>

## 2-1. SIngly LInked List : 단일 연결 리스트

> Head에서 Tail까지 단방향

- Head: 현재 노드

- Tail: 마지막 노드

![image](https://user-images.githubusercontent.com/79133602/159930492-d4e3aa46-1e95-430e-8824-0b6ac1593055.png)



시작과 끝이 있어 Tail의 포인터는 null/ 이후 노드만을 포인터에 저장

- 값을 찾을 때: 포인터를 순회하며 해당 노드가 원하는 값인지 찾기(선형시간-데이터 개수만큼)
- 값을 추가, 삭제 할 떄: 추가, 삭제할 놈에 연결된 이전, 이후 노드들의 포인터를 연결(상수시간)

<br/>

## 2-2. Doubly LInked List 

> 포인터가 이전, 이후 따로


![image](https://user-images.githubusercontent.com/79133602/159933151-dfdb1317-b230-4693-8c20-33711f5ccb0f.png)

이전 노드, 이후 노드가 무엇인지 포인트에 저장

<br/>

## 2.3 Circular LInked LIst 

> Tail이 Head로 연결됨

![image](https://user-images.githubusercontent.com/79133602/159933623-5e273767-1685-4bb9-a00b-22d60402331b.png)


<br/><br/><br/>

## 3. 스택 

> 선입 후출

![image](https://user-images.githubusercontent.com/79133602/159934136-94016edb-21fa-4b31-841b-f14e83343295.png)

ex. 스택 메모리 

자바스크립에서 구현하는 법 배열, 연결리스트 사용. 배열에 이미 pop,push가 있어서 배열로 사용하기가 편함

[스택에 관해서 참조](https://bellasimi.github.io/java/Java-Stack/)


<br/>
<br/><br/>

# 😎 번외 : Linked List 구현

> Singly Linked List


```
class Node {
  constructor(data){
    this.data = data;
    this.pointer = null;
  }
}

class SinglyLinkedList {

  constructor(){
     this.head = null;
     this.tail = null;
  }

  append(newVal){
    const newNode = new Node(newVal)
    if(this.head === null){
      this.head = newNode;
      this.tail = newNode;
    }else{
      this.tail.pointer = newNode;
      this.tail = newNode;
    }
  }

  find(val){
    let currNode = this.head; 
    while(currNode.data != val ){
       currNode = currNode.pointer;
    }
    return currNode;
  }

  insert(node,newVal){
    const newNode = new Node(newVal);
    //마지막 노드인지? node new Node로 수정 전 미리 묻기
    const boolean = node === this.tail;
    
    newNode.pointer = node.pointer;
    node.pointer = newNode;
    
    if(boolean){// 마지막 노드에도 insert 가능
       this.tail = newNode;
    }
    
   }
  
  remove(val){
     let preNode = this.head;
    const end = this.tail;
    while(preNode.pointer.data !== val){
       preNode = preNode.pointer; 
    }
    console.log(preNode)
    
    if(preNode.pointer !== end){
		//!==null이면 Tail 삭제가 안됨
       preNode.pointer = preNode.pointer.pointer;
    }else{//Tail의 값 삭제
       this.tail = preNode; 
    }
  }
  
  display(){
     let currNode = this.head;
    const end = this.tail;
    let arrStr = '[ '
    while(currNode != end ){
       arrStr += currNode.data + ', ';
      currNode = currNode.pointer;
    } //마지막 값 전에 끝나서
    arrStr+=end.data+' ]'; //마지막값 따로 추가 후 ]를 붙임
    
    console.log(arrStr)
  
  }
  
  size(){
     let currNode = this.head;
    const end = this.tail;
    let cnt = 1;
    while(currNode != end){
       cnt++;
      currNode = currNode.pointer;
    }
    return cnt;
  
  }


}

const list = new SinglyLinkedList();

list.append(1);// 1추가
list.append(2);
//console.log(list);
console.log(list.find(2));// 데이터가 2인 노드 찾기
list.insert(list.find(2),3)// 2 뒤에 3 추가
list.remove(3);
list.display();//[1,2]
console.log(list.size());//2
```
<br/><br/><br/><br/>

# 참고

💻 프로그래머스 데브코스 Day3 강의

💻 [MDN WEB DOCS: 자바스크립트 자료구조](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)
