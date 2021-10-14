<br/>
# 변수의 종류
<br/>
## 1.primitive type

원초적인 변수, 자바에서 제공하는 기본적인 데이터형의 변수입니다. 
기본값이 있기 때문에 null이 존재하지 않습니다. 그래서 class에서 int인 필드를 만들고 
<span style="color:red">null값을 넣으면 에러가 납니다.</span> 만약 null값을 넣고 싶다면 Object에서 호환되는 Wrapper Class를 
사용하면 됩니다. 
<br/>
| 자료형 | 예시 |
| :------- |:--------- |
| 정수형 | int,short int, long int |
| 실수형 | float, double |
| 바이트형 | byte |
| 논리형 |  boolean |
| 문자형 |  char |
<br/><br/>
## 2. reference type

Objec클래스를 직간접적으로 상속하며, <span style="color:red">null값을 받을 수 있습니다.</span>  Heap이란 메모리에 값의 주소값을 저장
합니다.  
<br/>
| 자료형 | 예시 |
| :------- |:--------- |
| 정수형 | Integer,Short,Long |
| 실수형 | Float, Double |
| 바이트형 | Byte |
| 논리형 |  Boolean |
| 문자형 |  Character,String |
<br/><br/><br/>
# 박싱과 언박싱

primitive type -> reference type 일때 박싱이라고 하며 reference type -> primitive type으로 변환할 때 언박싱이라고 합니다. 
이과정은 생성자 함수를 쓰고, 객체에 값을 가져오는 함수를 써서 직접 박싱 언박싱을 할 수도 있지만 그냥 값을 대입해 자동으로
처리할 수 있습니다. 
<br/>
'''
public void Wrpper() {
	
	Integer number = new Integer(1); //박싱
	int n = number.intValue();//언박싱	
	
	Integer number = 1;//자동 박싱
	int n = number;//자동언박싱
}

'''
<br/>
다만 두 변수의 값이 비교값과 일치하는지 확인할 때 reference type끼리는 equals()함수를 사용해야됩니다.

예로,
아래 코드를 보면

'''
public void Wrpper() {
	
	Integer number = new Integer(1); 
	Integer number2 = new Integer(1); 
	int n = 1;

	System.out.println(number==n); //true
	System.out.println(number.equals(n)); //true 
	System.out.println(number==number2)//false
	System.out.println(number.equals(number2))//true
}

'''
<br/>
* 1번,2번은 reference와 primitive를 비교
 == equals()모두 true로 잘 출력됩니다. 이는 두 자료간 비교는 컴파일러가 자동으로 박싱과 언박싱을 해주기 때문입니다. 
<br/>
* 3번째는 reference와 reference를 비교(==)
sysout에서 number와 number2의 값이 1로 같음에도 ==를 써서 false가 출력됩니다.
이는 ==가 래퍼 객체 내부의 값을 비교할 때 값이 아니라 참조 주소를 비교하기 때문입니다.  
두 객체(reference type변수들)은 참조 주소값이 비교대상이 되는데, 두 주소값이 다르므로 false가 나옵니다.    
<br/>

* 4번째 역시  reference와 reference를 비교(equals())
이번엔 equals()함수를 써서 주소에 담긴 값을 비교해 정상적으로 true가 출력됩니다. 
<br/><br/><br/>
# 참조

💻 <https://gbsb.tistory.com/6>

💻 <https://brunch.co.kr/@mystoryg/132>