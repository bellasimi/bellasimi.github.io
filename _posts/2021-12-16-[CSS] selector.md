---
title: 
sidevar:
  nav: "docs"
categories:
- css
tags:
- css
- selector
last_modified_at:
---

css에서 특정 요소의 디자인과 레이아웃을 바꾸고 싶을 때 해당요소를 선택하기 위해 selector를 사용합니다. 

<br/>
# selector 종류


> universal : 전체 선택자

HTML 페이지 내부의 모든 태그를 선택해줍니다. 

```
* { margin: 0; font-color: yellow}
```

이런식으로 지정해줄 경우 
웹페이지 태그간 margin 값은 태그 자체의 속성과 상관없이 0이 되고
글씨는 기본 노랑색이 됩니다. 

단 다른 태그 selector에서 다른 스타일 값을 준다면
universal 보다 특정 태그에 대한 selector 스타일이 우선적용됩니다. 


단점: universal 태그를 쓰면 모든 요소를 읽어내야 하기 때문에 페이지 속도가 
느려집니다.

그래서 margin이나 padding을 초기화할 때처럼 반드시 전체를 조작해야 하는 경우가
 아니라면 불필요하게 사용하지 않도록 합니다!


> type tag : 태그 선택자

HTML 태그를 직접 가져오는 선택자입니다. 

```
<h1>제목입력</h1>
<h1>큰글씨</h1>

/* CSS */

h1 { font-size: 12pt; }
```

HTML에서 지원하는 태그를 입력하면, 해당 태그로 입력된 모든 값의 스타일을 변경해줍니다. 
만약 h1의 글씨 크기를 12pt로 지정해 준다면, h1의 기본 글자 크기와 상관없이 
모든 h1태그의 글자 크기 값이 12pt로 변경됩니다. 


> #id : id 선택자 

단 한번 유일하게 사용되는 태그에 선택자로 id를 사용합니다. id명 앞에 #을 붙여서 css문서를 작성해주면 되는데요

```
<h1 id = "title">제목입력</h1>
<h1>큰글씨</h1>

/* CSS */

#title { font-size: 20pt; }
h1 { font-size: 12pt; }
```

똑같은 h1이어도 id는 달리 지정해서 스타일을 적용해 주기 때문에, 제목입력은 12pt가 아니라 20pt로 화면에 나옵니다. 


> .class : class선택자 

id와 달리 여러번 반복 가능한 selector로 class명 앞에 .을 붙여줍니다. 

```
<h1 id = "title">제목입력</h1>
<h1>큰글씨</h1>

<h1 class = "small">작</h1>
<h1 class = "small">은</h1>
<h1 class = "small">글</h1>
<h1 class = "small">씨</h1>

/* CSS */

.small { font-size: 8pt; }
#title { font-size: 20pt; }
h1 { font-size: 12pt; }
```


이제 작은 글씨라고 쓴 부분은 8pt로 출력되는데요, 만약 class 대신 id를 사용하면 
id는 중복이 불가능해서 오류가 납니다. 



> state : 상태 선택자 

특정 상태가 됐을 때 스타일 값을 변경해주는 선택자입니다. 

```
.small:hover {
      font-size: 40pt;			
}
```

만약 small이란 class에 hover; 마우스를 올리면, 글자크기가 40pt 가 됩니다. 



> attribute [] : 속성 선택자

태그중에 해당 속성가진 애만 변하게 해주는 선택자입니다. 


```
a[href] {
    a 태그 중링크 있는 애만 변함
}
a[href="AAA"] {
    AAA링크 있는 애만 변함
}
a[href^="AAA"] {
    AAA로 시작하는링크 있는 애만 변함
}
a[href$="AAA"] {
    AAA로 끝나는링크 있는 애만 변함
}

```

<br/><br/>
# selector 우선순위 

!important 선언을 사용한 형식이 가장 우선 순위가 높은데 이를 제외한 나머지는 다음과같은 우선순위를 가집니다.

> 전체선택자 - 태그선택자 - 클래스 선택자- ID선택자 - !important 
<br/>
## 복합선택자


단 복합 선택자를 갖는 경우엔 계산을 해야 되는데요.

```
li#list { font-size: 20pt; }

li.list { font-size: 10pt; }
```

이런 경우 같은 태그 선택자를 썼어도, 그다음 선택자가 id선택자> 클래스 선택자 순서이기 때문에 
li#list가 우선 적용됩니다. 

<br/>
## 우선순위를 모를 때


만약 스타일 우선 순위가 같거나 , 계산 방법이 없는 경우엔 마지막으로 지정된 스타일이 우선 적용됩니다.
예를 들어 자손 선택자와 자식 선택자가 부딫힐 경우, 우선 순위 계산법이 없기에 두선택자 중 마지막에 지정된 스타일이 적용됩니다. 


<br/><br/><br/>

# 참고

💻 <https://www.nextree.co.kr/p8468/>

