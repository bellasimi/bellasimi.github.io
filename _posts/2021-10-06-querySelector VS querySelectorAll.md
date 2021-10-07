<br/><br/>
[querySelectorAll사용법 보기](#queryselectorall)

class는 id와 달리 중복이 가능하죠. 그러다보니 같은 class값을 갖는 여러개의 요소를 선택해줘야되는 경우가 있습니다. 저는 오늘 아래와 같이 admin_menu class li를 2개 만들고 버튼이 클릭될시 active를 class 값에 추가해 css 적용하려합니다. 

![image](https://user-images.githubusercontent.com/79133602/136018756-42170fe3-ecd0-4b9a-9cdd-26b3aa2d6474.png)

아직 버튼에 addEventListner해주지 않은 상태입니다.

![image](https://user-images.githubusercontent.com/79133602/136019791-545a1a9c-11c8-4602-a721-364b73de1ff8.png)
<br/><br/><br/>

# querySelector


![image](https://user-images.githubusercontent.com/79133602/136019294-a308ef6f-2a26-40b0-8070-57aee17c5012.png)

먼저 querySelector로 해당 class값을 가진 요소를 선택해 변수선언해 줍니다. 

그리고
자바스크립트에서 버튼에 addEventListner 위와 같이 값을 넣어줍니다. 

이제, 버튼을 눌러서 이벤트를 실행하먼, 

![image](https://user-images.githubusercontent.com/79133602/136020309-9a807a95-a4e6-40cf-a009-37b3fcb44d54.png)

😥😥 첫번째 admin_menu에만 active가 적용된걸 볼 수 있습니다. 

왜 이런걸까요? 

원인은 바로 qrueySelect가 해당 값의 첫번쨰 요소만을 다루기 때문입니다. 그래서 여러개 요소를 선택할 때는 querySelectorAll()함수를 사용해줘야 됩니다. 
<br/><br/><br/>

# querySelectorAll

다만 querySelectorAll()을 사용할 땐 event를 반복해줘야 합니다. querySelectorAll()는 배열로 요소값을 가져오는데 반복문을 사용해서 해당 배열 각각의 값에 event를 발생하게 해줘야지 그냥 배열에 event를 주면 작동하지 않습니다. 

그래서 아래처럼 바꿔서 다시 실행시켜주시면 

![image](https://user-images.githubusercontent.com/79133602/136019427-62fe53bb-3a27-42e1-9ffe-e0f0b85b36b5.png)

모든 admin_menu의 class에 active가 추가된것을 보실 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/136020095-d67afd08-1e56-4701-b547-94585e351111.png)

