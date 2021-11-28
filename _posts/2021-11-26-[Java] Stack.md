---
title: Stack
categories:
	- java
tags:
- java
last_modified_at:
---

stack은 '쌓다', '더미'를 의미합니다. 

밑에서 위로 쌓이는 구조로 후입선출(선출후입) LIFO(Last In First Out)방식을 따라
가장 상단의 있는 데이터 Top부터 삭제 가능하며 순서를 무시한 채 
중간 또는 아래 데이터 부터 삭제하는 건 불가능합니다. 
<br/>
<br/>

# Stack 사용법
<br/>
생성자함수로 객체를 만들어 메소드에 접근할 수 있습니다. 
<br/>

| 메소드 | 기능 |
| :---: | :--- |
| **push(값)** | 값을 맨 위에 쌓아줍니다 |
| **pop()** | Top데이터를 삭제합니다 |
| **peek()** | Top데이터를 불러옵니다 |
| **search(값)** | Stack 내 값의 위치를 찾아줍니다 |
| **empty()** | Stack이 비었는지 boolean return |

<br/>
주로 쓰이는 함수들은 위와 같은데 
search()의 경우 위에서 아래로 데이터를 가져오는 Stack특성상
해당 값이 top의 위치 기준으로 얼마나 떨어져있는지를 알려줍니다.

Top데이터를 변수로 넣으면 -1이 나옵니다.
<br/>
예제를 통해 구체적으로 어떻게 쓰이는 지 알아보도록 하겠습니다. 

<br/>
## 1. push()

다음과같은 코드로 stack에 값을 넣어보겠습니다. 

```
        String s = "abcd";
        Stack<Character> stack = new Stack<Character>();
        for(char c: s.toCharArray()){
            stack.push(c);
            System.out.println(stack.peek());
        }
```

![image](https://user-images.githubusercontent.com/79133602/143578881-8c5bc131-5657-4f63-9414-93a111992a2c.png)


반복문 내 stack.push는 그림에 나온 것처럼 맨 처음으로 push된 'a' 가 가장 아래 놓이고, 마지막으로 push된 d가 Top데이터가 됩니다. 



<br/><br/>

## 2. pop() & peek()


```
        stack.pop();
        System.out.println(stack.peek());

```

![image](https://user-images.githubusercontent.com/79133602/143578922-6a9670ca-b16e-465c-8639-43911b3e46d8.png)

이때, pop()을 한 뒤 peek()한 내용을 출력하면, top 데이터 d가 삭제되고 새로운 top데이터가 된 c가 출력됩니다. 

<br/><br/>
## 3. search()


```
        System.out.println(stack.search('a'));//3
        System.out.println(stack.search('b'));//2
        System.out.println(stack.search('c'));//1
        System.out.println(stack.search('d'));//-1
```

<br/>

## 4. empty()

해당 stack에 'a','b','c'가 들어 있기 때문에 stack.empty()의 값은 false가 됩니다. 

<br/><br/><br/>

# 참고

💻 <https://docs.oracle.com/javase/7/docs/api/java/util/Stack.html>