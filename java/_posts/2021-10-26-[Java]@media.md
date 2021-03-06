---
categories:
- frontend
tags:
- css
- media
last_modified_at:
---

반응형 웹사이트 만들기위해 화면 크기마다 css달리 적용해줍니다.

# 문법 

```
@media *screen,speech,print,all*  <u>and,not,only,<u/> (화면크기){
	style 지정;
}

```
위처럼 @media 뒤에 기울임체로 써둔 요소들 중 하나를 입력-
 밑줄친 요소들중 하나를 입력 - ()안에 max-width: 1200px같은 화면 크기설정값을 입력 -
뒤에 {}하고 - {}안에 style값 넣기 


# 화면크기

기기마다 화면 크기가 다른데요. 보통 아래와 같습니다. 

mobile: 320~480px

tablet : 768~1024px

desktop: 1024~px


# 예시

```
@media screen and (max-width: 1200px) {
    #container #article img {
        margin-top: 10px;
        width: 100%;
        height: 100%;
    }
}
```

이런식으로 css 파일을 코딩하면, screen(화면)이 1200 너비가 된 시점부터 그 아래 화면에선 해당 style이 적용됩니다. 


# 참고

💻 <https://developer.mozilla.org/ko/docs/Web/CSS/Media_Queries/Using_media_queries>
