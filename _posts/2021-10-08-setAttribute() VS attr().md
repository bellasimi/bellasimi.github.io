
<br/>
태그의 속성값을 바꾸고 싶을 때 자바스크립트에선 setAttribute()를 제이쿼리에서는 attr()를 사용합니다. 자바스크립트와 제이쿼리의 문법이 다르므로 밑의 예제를 보면서 설명을 하도록 하겠습니다. 
<br/><br/><br/>

# setAttribute()

![image](https://user-images.githubusercontent.com/79133602/136371780-07ceb34e-76f8-4b58-be68-ebeef04d62aa.png)

자바스크립트는 요소를 선택할 때 id나 class명을 사용합니다. id일 때는 getElementById(), querySelector()함수를, class는  getElementByClassName(), querySelector()통해 요소를 선택할 수 있습니다. 

전 querySelector()요소를 가지고 왔는데요. getElement~ 함수들과 달리 ()안에 ('.class')('#id')이런식으로 id인지 class인지 식별자가 들어갑니다.

요소.setAttribute('속성','값'); 이렇게 입력을 하시면 해당 요소의 태그 중 제가 지정한 속성이 입력값으로 변합니다. 

여기서 전 원래 visibility: hidden으로 된 요소를 id가 admin일 경우 visible로 바꾸도록 했습니다. 
<br/><br/><br/>

# attr()

![image](https://user-images.githubusercontent.com/79133602/136371601-e103c4e6-2408-4f3e-b5f0-afe53b878fe7.png)

제이쿼리는 $()안에 요소의 id또는 class값을 바로 넣어주면 인식을 합니다. 간단한 문법이므로 굳이 변수설정을 해주지 않습니다. $('.class'), $('#id') 이런식으로 class와 id에 따라 식별자를 달리해서 넣어주신다음 요소.attr('속성','값');을 지정해 주시면 끝입니다. 

다만, 위에 스크립트에 최신 제이쿼리 링크를 걸어두셔야 됩니다. 그랬는데도 attr()등 함수를 인식하지 못한다면 node.js npm에 문제가 생긴 것이므로 [이포스트](https://bellasimi.github.io/%EC%A0%9C%EC%9D%B4%EC%BF%BC%EB%A6%AC-%EC%9D%B8%EC%8B%9D-%EC%98%A4%EB%A5%98/)를 확인해 주세요
<br/><br/><br/>

# 결과 

## 1. admin으로 접속할 경우

![image](https://user-images.githubusercontent.com/79133602/136375012-81bf1c62-ea3f-4114-8535-0c22ed169b6b.png)


## 2. 다른 아이디로 접속할 경우 

![image](https://user-images.githubusercontent.com/79133602/136374897-17de28f6-3ea7-422b-bd97-4a046f0aa819.png)
