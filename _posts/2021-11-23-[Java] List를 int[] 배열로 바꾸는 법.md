
다음과 같은 int[] nums를 List형으로 바꿨다가 다시 int[]형태로 바꾸려고 합니다. 

```
int[] nums = {1,2,3,4,5,6,7};
```

어떤 방법들이 있고, 그중에 가장 효율적인 방법은 무엇일까요? 

<br/><br/>

# int[] -> List<Integer>
<br/>
## 1. stream() 사용 
  
![image](https://user-images.githubusercontent.com/79133602/143009970-ace63ea3-a5a4-4a3d-ba15-8acccadb54f3.png)
  
stream()을 사용하는 경우 int를 Integer형태로 바꿔주기 위해서 boxed()메소드를 사용해야 합니다. 

그 후 래퍼클래스로 치환된 데이터를 collect(Collectors.toList())를 사용해 List로 묶어주시면 됩니다. 
<br/>
하지만 이 방법은 39024800ns가 걸리는 비효율 적인 방법입니다. 
  
<br/>
 ## 2. for문으로 직접 List에 add()
  
![image](https://user-images.githubusercontent.com/79133602/143010376-84ca4b1f-0a27-42b8-b428-9fafef6d47a3.png)
 
여기선 int형 데이터를 직접 넣을 수 있습니다. 소요시간은 53100ns로 stream()을 사용하는 방법보다 효율적입니다. 
  
  <br/><br/>

  
  
# List<Integer> -> int[] 
  <br/>
## 1. stream() 사용 
  
![image](https://user-images.githubusercontent.com/79133602/143011837-59f1a748-16b4-46c5-b6b1-a7cc2c330168.png)

Integer를 다시 int로 언박싱하기 위해서 stream().mapToInt() 메소드를 사용합니다. 

mapToInt()에 Integer::intValue를 넣으면 되는데, 이후 toArray()를 통해 int로 변환된 값이 배열로 바뀌도록 해줍니다. 

이방법으로 배열을 만들 때는 생성자 함수로 배열의 크기를 지정해 줄 필요가 없습니다. 
<br/>
반면 Integer[] 형태로 바꿀 때는 

```
Integer[] arr1 = list.toArray(new Integer[list.size()]);
```

언박싱하는 과정이 없지만 , 변수에 배열의 크기를 지정해 줘야 합니다.

<br/>
stream()을 사용하면   2171200ns의 시간이 소요됩니다. 아무래도 stream()은 마지막에 모든 중간연산을 
합친 후 합쳐진 연산을 최종으로 넘기기 때문에 시간이 오래걸리는 것 같습니다. 
<br/>
자세한 건 [반복문과 stream 속도 비교](https://medium.com/@jypthemiracle/java-stream-api%EB%8A%94-%EC%99%9C-for-loop%EB%B3%B4%EB%8B%A4-%EB%8A%90%EB%A6%B4%EA%B9%8C-50dec4b9974b) 참고

<br/><br/>
  
 ## 2. for문으로 직접 int[] 값 넣기
  
 ![image](https://user-images.githubusercontent.com/79133602/143011869-52771b30-7fd6-45f4-9219-dc0ca949903e.png)

이때도 언박싱 없이 list에서 get(인덱스)로 가져온 값을 해당 인덱스 배열에 넣어줄 수 있습니다. 시간은 41200ns로 훨씬 효율적입니다. 


<br/><br/>
# 결론 


stream은 가독성 유지보수에 있어서 장점이 있지만 시간이 너무 오래걸립니다. 

복잡한 로직이 담긴 함수를 구현해  순회비용보다 계산비용이 높은 경우가 아니라면, 
stream보다 for문으로 자료값을 바꾸는 것을 추천합니다. 





