<br/>
Math 클래스는 수학과 관련된 일련의 작업들을 쉽게 처리해주는 api들로 구성돼있습니다.
java.lang 패키지에 포함된 클래스이기 때문에 import가 필요없고 
메소드가 전부 static형태라 따로 객체를 생성할 필요가 없습니다. 오늘은 그중에서도 자주 쓰는 메소드들에 대해 알아보도록 하겠습니다.
<br/>
<br/>

## 1. Math.round()

반올림을 해주는 메소드로, 반환값이 int형입니다. 따라서 1.5를 넣어도 아래처럼 2로 출력됩니다. 

```
        Math.round(1.2);//1
        Math.round(1.5);//2
        Math.round(1.7);//2
        Math.round(1);//1
        Math.round(-1.2);//-1
        Math.round(-1.5);//-1
        Math.round(-1.7);//-2
```
<br/>
## 2. Math.ceil()

올림을 해주는 메소드로 실수형을 반환합니다. 따라서 소수자리를 버린 뒤에도 .0이 뒤에 붙습니다. 0.5를 넘지 않아도 소수자리를 버리고 +1하기 때문에
위와 달리 1.2, 1.3 모두 2.0이 됩니다. 

```
        Math.ceil(1.2);//2.0
        Math.ceil(1.5);//2.0
        Math.ceil(1.7);//2.0
        Math.ceil(1);//1.0
        Math.ceil(-1.2);//-1.0
        Math.ceil(-1.5);
        Math.ceil(-1.7);
```
<br/>
## 3. Math.floor()

내림을 해주는 메소드로 실수형을 반환합니다. 


```
        Math.floor(1.2);//1.0
        Math.floor(1.5);
        Math.floor(1.7);
        Math.floor(1);
        Math.floor(-1.2);//-2.0
        Math.floor(-1.5);
        Math.floor(-1.7);
```
<br/>
## 4. Math.abs() 

절대값을 구하는 메소드로 기존 자료형에 맞게 양의 형태로 반환해줍니다. 

```
        Math.abs(-1.2);//1.2
        Math.abs(-2);//2
```
<br/>

## 5. Math.pow(a,b)

a의 b제곱 값을 구해 실수형으로 반환해 줍니다. 변수값으로 int가 들어와도 되지만 int의 int제곱을 해도 반환이 실수형이라
정수형으로 바꿔야 할 때는 (int) 캐스팅을 해주면 됩니다.

```
        Math.pow(2.0,3.0);//8.0
        Math.pow(2.0,3);//8.0
        Math.pow(2,3)//8.0

```
<br/>

## 6. Math.sqrt()

제곱근을 구하는 함수로 실수형을 반환합니다. 

```
        Math.sqrt(4.0);//2.0
        Math.sqrt(4);//2.0
```
<br/>

## 7. Math.max(a,b) & Math.min(a,b)

a,b중 최대 최소값을 구해주는 함수인데, 비교대상의 자료형으로 결과값을 반환해 줍니다. 그래서 아래처럼 
Math.max(2.0,4);는 최대값이 4인데 도출된 값은 4.0 실수 형입니다.


```
        Math.min(2,4);//2
        Math.max(2,4);//4
        Math.min(2,4.0);//2.0
        Math.max(2.0,4);//4.0
```
<br/>

## 8. Math.random()

0~1.0까지 범위에서 난수값을 구해줍니다. Random클래스의 nextInt(1.0);과 같은 역할입니다. 여기서 1.0은 포함되지 않습니다.
만약 원하는 범위가 a라면 Math.random()*a; 이런식으로 나타내주면됩니다.

```
        double a = Math.random() * 10;//0~9.0
        int ai = (int)Math.random() * 10;//0~9
        double b = Math.random()*11;//0~10.0
        int bi = (int)Math.random()*11;//0~10
        char c = (char)((int)Math.random()*26+'a');//0~25+a->char반환 아스키코드상 a와 z가 25차이가 남  
```

<br/><br/><br/>
# 참고

💻 <https://docs.oracle.com/javase/8/docs/api/>