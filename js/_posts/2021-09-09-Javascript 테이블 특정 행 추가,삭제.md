
![image](https://user-images.githubusercontent.com/79133602/132698721-efe3df9e-fc01-44e6-8538-7b31bdbe058f.png)


# 1. 테이블 지정 
 	const table = document.getElementById('테이블의 id');

# 2. 테이블에 행 추가하기 : 테이블.insertRow(행:인덱스);
![image](https://user-images.githubusercontent.com/79133602/132699061-2b93a94b-92a4-4d24-8cc0-bf5d4c65ee7a.png)

* 0번째 댓글 밑에 댓글 폼이 나오길 원하면 insertRow() 함수 안에 인덱스+1을 변수로 넣어주면 된다.

![image](https://user-images.githubusercontent.com/79133602/132699298-d39ce53e-2a4d-468c-91c7-f3e16e8c9c90.png)

*그럼 이런식으로 아래 칸에 행이 추가된다. 

# 3. 행에 들어갈 열 넣어주기 : 행.insertCell(열);
* ()의 값은 열을 의미한다. 
*기존 테이블 보다 큰 값을 넣으면 에러가 난다. 

# 4. 새로운 행의 열에 들어갈 값 넣어주기 : 해당칸 변수 = 행.insertCell(열)
* 변수. innerText = "원하는 값" : 텍스트를 넣을 수 있다. 
* 변수. innerHTML= "원하는 값" : HTML값을 넣을 수 있다. 







