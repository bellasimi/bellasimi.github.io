아래와 같이 int[] 배열이 있을 때, 서로 다른 두 인덱스의 합을 저장한 뒤 오름차순 정렬을 하려고 합니다. 

단 중복은 허용되지 않습니다.

```
 int[] arr={2,1,3,4,1};
```

이 경우에 int[] 배열은 서로 다른 두 인덱스의 합이 몇가지가 나오는지 계산하고, 
중복값을 걸러내는데 어려움이 있습니다.

그래서 자체 method로 그과정을 간단히 해줄 Collection 인터페이스의 Set, List를 사용하는게 좋습니다.
<br/>
각각 어떤식으로 값을 구하고 차이는 무엇인지 알아보도록 하겠습니다.

<br/><br/>


# Set<E>

중복이 불가능하고 값의 저장순서가 보장되지 않습니다.  Set클래스는 추상클래스이기 때문에 생성자함수를 만들 수 없어 
자식클래스인, TreeSet<E>의 생성자 함수를 사용합니다. 

<br/>
HashSet<E>은 해시 알고리즘을 사용해 빠른 속도를 가졌지만 정렬이 되진 않고 

TreeSet<E>은 이진 검색트리를 사용해 자동 오름차순 정렬이 되지만 HashSet에 비해 속도가 느립니다. 
<br/>

```
        TreeSet<Integer> ts = new TreeSet<Integer>();
       
         for(int i=0;i<arr.length;i++){
             for(int j=0;j<arr.length;j++){
                 if(i!=j){
                     ts.add(arr[i]+arr[j]);

                 }
             }
         }

        System.out.println("걸린시간 : "+(end-start));//1300
        System.out.println(ts);//[2, 3, 4, 5, 6, 7]


        Set<Integer> set = new HashSet<Integer>();

        for(int i=0;i<arr.length;i++){
            for(int j=0;j<arr.length;j++){
                if(i!=j){
                    set.add(arr[i]+arr[j]);
                }
            }
        }
        System.out.println("걸린시간 : "+(end-start));//800
        System.out.println(set);//[2, 3, 4, 5, 6, 7]*/

```
<br/>
만약 저장된 순서를 보장하고 싶다면 LinkedHahSet<E>을 사용하시면 됩니다.
<br/><br/>

# List<E>

중복이 가능하고, 값이 add()된 순서로 저장됩니다. List<E>역시 추상클래스 이기때문에 ArrayList<E>등의 자식클래스의 생성자 함수를
사용합니다. 단, 중복을 거르고 정렬을 하기 위해 추가 메소드를 사용해야 되서 속도가 느립니다. 


```
        List<Integer> list = new ArrayList<Integer>();
        for(int i=0;i<arr.length;i++){
            for(int j=0;j<arr.length;j++){
                if(i!=j){
                    list.add(arr[i]+arr[j]);
                }
            }
        }

        System.out.println("걸린시간 : "+(end-start));//600
        System.out.println(list);//[3, 5, 6, 3, 3, 4, 5, 2, 5, 4, 7, 4, 6, 5, 7, 5, 3, 2, 4, 5]

        list = list.stream().distinct().sorted().collect(Collectors.toList());
        System.out.println("걸린시간 : "+(end-start));//38597200
        System.out.println(list);//[2, 3, 4, 5, 6, 7]

```

List의 경우 중복값 제거를 위해 stream()의 distinct()메소드를 이용해줍니다. 그리고 sorted()로 오름차순 정렬 후 stream된 객체를
collect(Collectors.toList())를 통해 다시 List 형태로 바꿔줍니다.
<br/>
만약 int[]형태로 바꾸고 싶다면

```
        int[] change = list.stream().distinct().sorted().mapToInt(Integer::intValue).toArray();
```

위와 같이 코드를 짜주시면 됩니다. 

<br/>
하지만 List로 값을 구하면 Set으로 구할 때 보다 무려 38596000ns나 더 오랜 시간이 걸립니다.😢

코드도 더 길고 비효율 적이죠.
<br/>
그래서 저장순서가 중요하거나 중복값 제한이 없는 경우 사용하는 게 좋습니다. 
그냥 add만 하는 경우라면 위처럼 List가 더 처리 속도가 빠르니까요.

<br/><br/><br/>



# 참고

💻 <http://www.tcpschool.com/java/java_collectionFramework_set>

💻 [List,Map,Set 비교](https://cocoon1787.tistory.com/527)

💻 [Collection이란?](https://crazykim2.tistory.com/557)