특정 요소를 다양한 방식으로 변형할 때 사용합니다. 특히 transition함수 3d 기능과 함께 사용할 시 효과가 배가 되는데 
이를 @keyframes을 통해 섞어 사용하면 애니메이션효과를 줄 수 있습니다. 



## 1. 확대, 축소 

* transform:scale(x축비율,y축비율); x축,y축 확대, 축소

* transform:scaleX(x축비율); x축 확대, 축소

* transform:scaleY(y축비율); y축 확대, 축소



## 2. 회전

* transform:rotate(n); n도 만큼 회전

* transform:rotateX(n); x축으로 n도 만큼 회전

* transform:rotateY(n); y축으로 n도 만큼 회전



## 3. 이동

* transform:translate(x,y); x축으로 x크기만큼 이동, y축으로 y만큼이동

* transform:translateX(x); x축으로 x크기만큼 이동

* transform:translateY(y); y축으로 y만큼이동


'''
transform: translate(-50%,-50%);//x축 50% 반대 이동, y축 50% 반대 이동 -> 중간에 위치 
transform:translateX(-8px); //x축 좌측으로 8px이동
transform:translateX(8px); //x축 우측으로 8px이동

'''


## 4. 기울이기

* transform:skew(xn,yn); x축으로, y축으로 n도만큼 기울이기

* transform:skewX(xn,yn); x축으로n도만큼 기울이기 

* transform:skewY(xn,yn); y축으로 n도만큼 기울이기  



# 참고

💻 https://webclub.tistory.com/619

💻 [https://www.biew.co.kr/](https://www.biew.co.kr/entry/CSS3-Transform-%EC%86%8D%EC%84%B1-scale-rotate-translate-skew-%EC%8B%A4%EB%AC%B4%EC%98%88%EC%A0%9C-%EC%B2%A8%EB%B6%80%ED%8C%8C%EC%9D%BC-%ED%8F%AC%ED%95%A8)