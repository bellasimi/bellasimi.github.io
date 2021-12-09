---
title: 
categories:
- java
tags:
- Comparator
last_modified_at:
---
아래와 같은 값을 가진 Map 클래스 객체 map이 있습니다. 


```
Map<Integer,Double> map = new HashMap<Integer, Double>();
//[1=0.125, 2=0.42857142857142855, 3=0.5, 4=0.5, 5=0.0]

List<Map.Entry<Integer,Double>> list = new LinkedList<>(map.entrySet());

```

현재 key값으로 오름차순 정렬이 됐는데요. 

value로 내림차순 정렬을 하고, value가 같다면 key값으로 오름차순 정렬을 하려면 어떻게 해야 할까요? 


<br/><br/>
# Comparator 클래스 사용

일단 가장 좋은 방법은 Comparator 클래스의 compare()함수를 @Override로 재정의하는 방법입니다. 
<br/>
HashMap은 순서가 존재하지 않기 때문에 이방법을 쓰기 전에 List에 map담아줘야 합니다. 
<br/>
<Key,Value> 형태를 유지한 채 정렬을 하기 위해서 list의 자료형으로 Map.entry 인터페이스를 사용할텐데, 
이는 map의 key와 value를 조회하는 메소드를 제공합니다.  

그리고 생성자에 map.entrySet()을 넣어 
모든 map값을 list에 입력합니다. 


```

/* 내림차순을 해주기 위해 List화 */
        List<Map.Entry<Integer,Double>> list = new ArrayList<>(map.entrySet());

/* value기준 내림차순, 인덱스 기준 오름차순 정렬 */
        Collections.sort(list, new Comparator<Map.Entry<Integer,Double>>(){
            @Override
            public int compare(Map.Entry<Integer,Double>o1, Map.Entry<Integer,Double>o2){
                if(o2.getValue()-o1.getValue()>0){//첫번째 param < 두번째 param
                    return 1;//o2가 큰경우 1
                }
                if(o2.getValue()-o1.getValue()<0){//첫번째 param > 두번쨰 param
                    return -1;//o1이 큰경우 -1
                }
                return o1.getKey()-o2.getKey(); //값이 같으면 key값을 오름차순으로
            }

        });

        System.out.println(list);

```

compare(o1,o2)함수가 인자 두개를 비교를 하는데 우리는 Map.Entry<Integer,Double>를 비교 하는거라
위처럼 클래스를 입력합니다. 

그리고 함수를 재정의 하는 조건문 내에서 비교대상이 map의 value이므로

o1.getVaule()를 사용하고, 내림차순이라 o1의 값이 작을 때 양수를 o1의 값이 클때 음수를 반환해줍니다. 

같을 때는 o1.getKey()-o2.getKey(); 사용 o1의 키값이 클 때 양수, 작으면 음수 같으면 0을 반환해 오름차순이 되게 해줍니다.
<br/>

# 💥 주의: overflow

현재는 key값이 1~5라 overflow가 되지 않는데 
<br/>
만약 o1이 -2,147,483,648이고  o2가 1이라서 
-2,147,483,648 - 1 = -2,147,483,649로 int 자료형을 벗어날 거 같으면 조건문으로 대소비교후 각각 1,0,-1을 반환하는 것이 안전합니다. 

<br/>
<br/>

# 결과 


```
//정렬 전
[1=0.125, 2=0.42857142857142855, 3=0.5, 4=0.5, 5=0.0]

//정렬 후
[3=0.5, 4=0.5, 2=0.42857142857142855, 1=0.125, 5=0.0]

```


<br/>
<br/>

# 참고

💻 [Comparable과 Comparator의 이해](https://st-lab.tistory.com/243)

💻 [java api8: Comparable](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html#method.summary)

💻 [java api8: Comparator](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#method.summary)

💻 <https://hianna.tistory.com/569>

💻 [생활코딩: Map](https://edu.goorm.io/learn/lecture/41/%EB%B0%94%EB%A1%9C%EC%8B%A4%EC%8A%B5-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9-%EC%9E%90%EB%B0%94-java/lesson/39124/map)