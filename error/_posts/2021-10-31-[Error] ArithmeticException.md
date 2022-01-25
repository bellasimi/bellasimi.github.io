---
title: 
categories:
tags:
- error
last_modified_at:
---

```
    public static void main(String[]args){
        Scanner sc = new Scanner(System.in);
        int [] arr ={1,2,3,4,5};
        for(int i=0;i<arr.length;i++){
            System.out.println(arr[i]/i);
        }

    }

```
해당 배열의 값을 가져와서 인덱스의 값으로 나눈 값을 출력하는 코드를 짰는데 아래와 같은 오류가 떴습니다. 


![image](https://user-images.githubusercontent.com/79133602/139581788-6ea75992-b595-48e4-a206-feb33b6943cf.png)


원인이 무었일까요?🤔
<br/><br/>

ArithmeticException는 0으로 값을 나눴을 때 발생합니다.

저 같은 경우 인덱스가 0인 값을 가져오려고 i를 0부터 시작하게 한게 원인이었습니다. 

그렇다면, 0행을 가져오면서 0으로 나눈 값 0을 도출하면서, arr[i]/i 식을 사용할 수 있는 방법은 없을까요?

<br/><br/>
# 해결방법

아래처럼 조건문을 줘서 index가 0경우에만 0이 도출되게 하면 됩니다. 


```
    public static void main(String[]args){
        Scanner sc = new Scanner(System.in);
        int [] arr ={1,2,3,4,5};
        for(int i=0;i<arr.length;i++){
            int answer = i>0? arr[i]/i:0;
            System.out.println(answer);
        }
    }
    
```

