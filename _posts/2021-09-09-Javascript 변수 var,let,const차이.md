# var
![image](https://user-images.githubusercontent.com/79133602/132686818-65d9cf13-832f-4603-86e0-35bef5fa7b3e.png)
* 변수 선언을 여러번 할 수 있다.
![image](https://user-images.githubusercontent.com/79133602/132687226-ee716057-dbd6-4bce-87d3-9d288ad9b469.png)
* hoisting시 선언문 이전에 참조가능하다. ; hoisting(선언문을 해당 스코프의 선두인 것처럼 동작하는 것)
* 간단하게 변수를 테스트할 땐 편할 수 있지만 코드량이 많아지면 값을 파악하기 힘들다. 
* 외부에서 접근이 가능해 보안에 취약하다. 

* var의 단점을 보완하기 위해 ES6이후 아래의 변수선언 방식이 추가됐다. 

# let
![image](https://user-images.githubusercontent.com/79133602/132688299-6b6da702-1b93-49a4-b924-0401dd23e4bc.png)
![image](https://user-images.githubusercontent.com/79133602/132688108-47b1c77f-66fc-498c-98d2-487eb2e8dcd9.png)
* 변수 선언을 여러번 할 수 없다. -> 2번째 let id에 빨간줄이 그어진 이유 
* hoisting시 선언문 이전에 참조 불가능하다. -> 처음 console.log는 변수 선언문 전에 나와 에러가 남
* 이는 let이 변수의 생성단계가 var와 다르기 때문이다. 
* var: 변수선언, 초기화> 할당; 선언과 초기화가 한번에 VS let: 변수선언 > 초기화 > 할당; 선언과 초기화 단계가 분리
* 즉 메모리 공간확보와 undefined로 초기화가 되지 않아 hoisting이 불가능한 것!

![image](https://user-images.githubusercontent.com/79133602/132688470-5ae34ee0-9432-48ba-9668-aaefb687641d.png)
* 단 재할당은 가능하다. -> 위 경우에 재할당된 자바스크립트가 log에 찍힌다.

# const
![image](https://user-images.githubusercontent.com/79133602/132690392-c414b741-609a-4d60-a7b3-877fe272abed.png)
* 변수 선언도 1번 할당도 1번만 가능하다. 
* 보안에 유리

# 변수 선언 방식 선택
* 일단 보안에 취약하고 값을 일정하게 유지하는데 단점이 있는 var는 배제
* 기본적으로 const를 사용하고 재할당이 필요한 경우에 let을 사용하는 것이 좋다. 



# 참조
< https://www.howdy-mj.me/javascript/var-let-const/ >
< https://poiemaweb.com/es6-block-scope >