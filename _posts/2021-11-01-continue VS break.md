---
title: 
categories:
- java
tags:
- continue
- break
last_modified_at:
---
<br/>
반복문을 사용할 때 모든 경우를 다 돌아야 할까요? 🤔

만약 항상 그런식으로 작업을 한다면 시간도 오래걸리고 자원소모도 큽니다. 
그래서 조건에 만족하는 첫번째 답만 찾는 경우엔
해당 조건을 만족하는 값을 찾고 반복문을 빠져나갈 수 있게 **break;**해줘야 합니다. 

하지만 반대로, 조건을 만족하는 값을 여러개 찾아야 하거나, 반복되는 작업을 수행해 줘야 하는 경우엔 
조건을 만족해도 반복문을 빠져나가지 않도록 **continue;**해줘야 합니다. 

그렇다면, 어떤식으로 사용되는지 아래 예시를 보면서 구체적으로 살펴보도록 하겠습니다. [요약만 보기](#요약)

<br/>
<br/>


# break



```
public class ContinueBreak {
    public static void main(String[]args){
        int[] arr ={1,2,3,4,5,6,7};
        int i=0;
        while(i<arr.length){
            if(arr[i]==4){
                System.out.println("4입니다.");
                break;
            }
            i++;
        }
        System.out.println(i);
    }
}

```

int배열에 {1,2,3,4,5,6,7} 값이 들어있는데, 해당 배열의 길이만큼 반복문을 돌립니다. 배열이 돌아갈
 때마다 i가 1씩 증가합니다. 여기서 배열에 든값이 4면 반복문을 break를 써서 종료하는데, 

![image](https://user-images.githubusercontent.com/79133602/139703884-ab61a423-a5e0-4294-825e-a489924d566d.png)


그러면  arr[3]일때 종료가 됐기때문에 "4입니다."출력후
그 뒤의 i++없이 loop를 빠져나와 i값은 3으로 출력됩니다.

이제 arr의 값이 4인 조건외에 5인 조건도 출력해보겠습니다. 반복문 안에 아래 코드만 덧붙였는데요.

```
            if(arr[i]==5){
                System.out.println("5입니다.");
                break;
            }
```

결과는 당연히 실패, 
해당 조건만 만족하면 반복문을 나가는 break 때문에 또다른 조건문을 실해하지 않고 반복문을 나가버립니다. 

<br/><br/>

# continue

그래서 continue를 사용해줘야 합니다. 그래야 반복을 계속 진행해서 그다음 조건문도 실행할 수 있습니다. 


```
public class ContinueBreak {
    public static void main(String[]args){
        int[] arr ={1,2,3,4,5,6,7};
        int i=0;
        for(i=0;i<arr.length;i++){
            if(arr[i]==4){
                System.out.println("4입니다.");
                continue;
            }
            if(arr[i]==5){
                System.out.println("5입니다.");
                break;
            }
        }
        System.out.println(i);
    }
}

```

![image](https://user-images.githubusercontent.com/79133602/139709499-9046cf0c-6487-40ea-97eb-dc84e6f649e9.png)


여기서 모든 인덱스를 출력하고 싶다면, 2번째 조건도 continue를 해주시면 됩니다. 이때는 모든 배열을 다 도는 거라, 위 두 과정 보다
시간과 자원소모가 큽니다.  


![image](https://user-images.githubusercontent.com/79133602/139707165-79336da9-3aff-4db5-9123-87ba245410d9.png)


<br/>

* 주의점
 인덱스 증가를 위해 i++를 해줘야되는데 조건문이 continue다음 i++로가지 않고 조건문 앞으로 가다보니, i<arr.length가 무한 참이돼 루프에 갖히게됩니다. 
이를 방지하려면 for문을 쓰거나  int i=0으로 초기화하시고  조건문위에 i++;하셔야합니다. 
<br/><br/><br/>

# 요약

## break

* 조건을 만족하면 바로 반복문 종료
* 이중 반복인 경우엔 현재 위치의 반복문만 빠져나올 수 있음

## continue

* 조건을 만족했어도 반복문을 계속 진행
* continue후 조건문 위로 올라가기 때문에, 해당 조건을 만족하는 경우에 한해 조건문 아래 코드를 실행 x


```
        for(int i=1;i<7;i++){
            if(i%2==0){
                continue;
            }
            System.out.println(i);
        }

```

이런 경우 짝수는 아래 코드를 실행하지 않아서 홀수만 찍힘 



