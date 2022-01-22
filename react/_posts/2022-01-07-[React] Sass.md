---
title: 
sidevar:
  nav: "docs"
categories:
- react
tags:
- react
- sass
- css
last_modified_at:
---

Sass는 css를 프로그래밍언어스럽게 작성하도록 도와주는 preprocessor 패키지입니다. 
예로 sass를 사용하면 css 파일 내에서 변수, 연산자, 함수, extend import등을 사용해 코딩이 가능합니다.

그런데 브라우저는 sass문법을 몰라서 sass로 작성한 파일을 다시 css로 컴파일해야됩는데요

그러기 위해서 다음과 같이 node-sass 라이브러리를 설치해 줍니다. 

```
Yarn add node-sass
Npm install noe-sass
```

<br/><br/>
# CSS 기존 방법과 차이

기존에 css만을 사용해 스타일을 적용할 땐, 아래 같은 화면의 Detail 글씨의 배경색을 지정하기 위해 아래와 같은 과정을 거쳐야 했죠.

![image](https://user-images.githubusercontent.com/79133602/148521727-23d862a5-7bf7-4cbf-a5c2-3fdd3b68b3f9.png)

스타일 적용할 태그에 className="black" 이라고 쓰고 아래처럼 css를 작성후

```
.black {
	Background-color: black;
}
```
해당 컴포넌트 함수 파일에 해당 css파일을 import 해주면

```
Import 'Detail.css';

```
아래처럼 css 스타일이 적용됐는데요.


![image](https://user-images.githubusercontent.com/79133602/148521765-e9228591-42b5-47a3-a1bd-3b04a5c76349.png)


지금은 간편하지만 코드가 길어지면 일일이 스타일 설정을 나열해야 되고, 설정값도 black은 단순하지만
그보다 복잡한 값을 쓸 땐 기존 방법이 불편합니다. 

이를 개선할 수 있는 차이점들이 Sass엔 존재합니다. 

아래의 Sass 문법들을 보면서 알아보도록 하겠습니다. 

<br/>
# Sass 

먼저 Sass 문법 쓰고 싶다면 아까 상단에 언급했던 node-sass 설치가 끝나 있어야 합니다. 설치가 됐다면,
 .css 파일을 .scss로 바꿔주세요 그리고 scss로 다시 import 해주세요
 
![image](https://user-images.githubusercontent.com/79133602/148521802-17242089-baad-418b-bbb1-93b9f4b0acd0.png)

<br/><br/>
## 1. 변수사용

Sass는 복잡한 값을 변수에 넣을 수 있는데요. $입력후 변수명을 기입 : 다음에 값을 입력하면 됩니다.

![image](https://user-images.githubusercontent.com/79133602/148521833-ce7aa7a4-268d-4ac5-8625-0d05f4385180.png)

#ffff11처럼 계속해서 입력하기 어려운 값들이 반복될 때 직관적인 이름의 변수에 값을 담아주면
코딩이 편해지죠. 


<br/><br/>
## 2. @import 파일경로

@import 명령어를 사용하면 css끼리 import가 가능합니다.


![image](https://user-images.githubusercontent.com/79133602/148521866-65e2a79f-dc2d-4562-9a1a-288a80979668.png)

해당 파일은 Detail.scss에서 import하기 위해선 다음 코드를 입력하시면 됩니다.

```
@import './reset.scss';
```

![image](https://user-images.githubusercontent.com/79133602/148521899-146f047a-4bcc-4d1d-8c02-50fed3689bd9.png)

그러면 글씨가 전부 reset.scss에서 지정한대로 바뀝니다.


* 쓸데없는 파일들은 _작명 이런 이름을 갖습니다. 그럼 컴파일을 자동적으로 하지 말라는 뜻입니다. 


<br/><br/>
## 3. nesting

하위 selector를  일일이 나열하지 않고 상위 selector의 중괄호 안에 다 모아서 쓸 수 있게 해주는 기능으로 코드가 길어질 때 가독성을 높여줍니다.

![image](https://user-images.githubusercontent.com/79133602/148521955-f1557bf6-8d69-430d-8a15-1e454b9a6c74.png)

![image](https://user-images.githubusercontent.com/79133602/148521969-8905e8b2-9233-4a47-bb6e-42bb2d070aa0.png)

<br/><br/>
## 4. @extend

![image](https://user-images.githubusercontent.com/79133602/148522000-bec536e4-81fd-4d8e-82e9-9e98df6585ae.png)


현재 위 페이지에 다음과 같은 css를 적용하고 있는데, 만약 해당 div에 다른 css를 번갈아 가면서 적용하려면 어떻게 할까요?

![image](https://user-images.githubusercontent.com/79133602/148522043-2a93d166-05fb-4116-be3f-7c3f7cc89d95.png)

전엔 className을 새로 만든 뒤 내용을 전부 써줘야 했죠.

![image](https://user-images.githubusercontent.com/79133602/148522065-c0c12e3d-a1aa-4251-b60d-5f179fbcdbcc.png)

그러면 위처럼 하나를 바꿀 때도 작성해야 되는 코드의 양이 많아서 비효율적이었습니다. 

이제 @extend를 사용하시면

![image](https://user-images.githubusercontent.com/79133602/148522112-5141e142-59ef-4521-96dd-722d1fd78f75.png)

바꾸고 싶은 부분만 코딩하고 나머지는 @extend를 통해 css를 복사해오시면 됩니다. 

![image](https://user-images.githubusercontent.com/79133602/148522153-e6887265-98ea-4560-bc3a-39c3296777df.png)

<br/><br/>
## 5. @mixin/ @include

Css를 함수화해서 다른 selector가 함수를 사용할 수 있게 해주는 기능입니다. 
아래처럼 @mixin 함수명() 으로 css 함수를 만들고 원하는 selector에서 쓸 땐 @include 사용하고자하는 함수명을 코딩해주시면 됩니다.

![image](https://user-images.githubusercontent.com/79133602/148522182-cb3d2768-45a2-410b-acde-ad25897dfd6a.png)
