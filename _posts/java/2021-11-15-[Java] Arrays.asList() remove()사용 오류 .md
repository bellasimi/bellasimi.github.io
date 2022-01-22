---
title: 
categories:
- error
tags:
- ArrayList
- error
last_modified_at:
---
![image](https://user-images.githubusercontent.com/79133602/141796823-b8af1401-3028-45a4-a886-59d3f1594fc5.png)

오늘 만난 에러입니다. 

![image](https://user-images.githubusercontent.com/79133602/141801567-28ff03cb-510f-4eda-a1a6-50fbb716de85.png)

배열을 리스트로 만들고 출력하는 것 까진 잘 됐는데 
이 리스트 값에 List클래스의 remove() 메소드를 사용하려고 할 때 오류가 나고 있습니다. 😥

![image](https://user-images.githubusercontent.com/79133602/141801284-6d0c9744-ee5b-4aa4-8f02-76621ad5e1fd.png)


# 원인

Arrays.asList로 생성한 List 값은 고정된 사이즈의 값이라 원소 제거가 되지 않습니다. 

그리고 Java api를 참조하면 알겠지만,

remove()는 java.util.ArrayList의 메소드로 java.util.arrays.ArrayList에선 지원하지 않습니다. 

따라서 위와 같은 오류가 발생한 거죠.



# 해결 방법

![image](https://user-images.githubusercontent.com/79133602/141800890-ef9a81c7-24d5-481f-84e6-6a37f3b8bc02.png)

Arrays.asList로 만든 List를 ArrayList의 생성자 함수 값에 넣어주면 됩니다. 그러면 아래처럼 remove()를 했을 때 오류 없이
결과가 잘 출력됩니다. 

![image](https://user-images.githubusercontent.com/79133602/141801013-4cf53fea-8c3d-4111-8f8e-41b684790030.png)