---
title: 
categories:
- blog
tags:
- blog
last_modified_at:
---
블로그 제작 사이트를 통해 블로그를 생성한 경우 웹페이지가 자동으로 공개되지만 직접 블로그를 만들어 배포한 경우라면 그렇지 않습니다.
😢 

따라서 직접 노출이 되도록 설정을 해줘야 하는데 오늘은 Google 검색 노출에 대해 알아보도록 하겠습니다.


---
# 🔍 목차

[1. Google Search Console](#1-google-search-console)

[2. 소유권 확인](#2-소유권-확인)

[3. sitemap.xml 생성](#3-sitemap파일-생성)

[4. robots.txt 생성](#4-robots파일-생성)

[5. sitemap.xml 등록](#5-sitemap파일-등록)

---

구글 검색 원리를 알고 싶다면 [여기](https://www.google.com/intl/ko/search/howsearchworks/)를 눌러주세요


## 1. Google Search Console

먼저 [구글 서치 콘솔](https://search.google.com/search-console/about)접속합니다.

![image](https://user-images.githubusercontent.com/79133602/140523027-9313c896-77c7-4b45-99b5-eabe1b36f7f0.png)

시작하기 버튼을 누른 후, 사용할 계정으로 로그인하면 아래와 같은 화면이 나오는데,

![image](https://user-images.githubusercontent.com/79133602/140523497-ab22c9a7-c8dd-4d0d-80cf-2bd83859ac2d.png)

왼쪽은 도메인이 있는경우고 오른쪽은 없는경우 입니다.

깃허브 블로그는 도메인 없는 오른쪽이기에 위처럼 입력해주고 계속을 누르시면 됩니다.

도메인으로 할 경우 http 또는 https따로 등록 안하셔도 되고 dns인증만으로 끝난다고 하니 있으신 분은 편리한 왼쪽을 사용하시면
되겠습니다.

<br/>
<br/>

## 2. 소유권 확인


그러면 소유권 확인이 뜨는데,

![image](https://user-images.githubusercontent.com/79133602/140524257-145fc316-a052-4460-8961-ac6af4d5dadb.png)

아래 다섯 가지 방법 중 어떤 방법으로 소유권을 확인할지 선택해야 합니다.

1. HTML 파일 다운로드

2. HTML 태그 추가

3. Google 애널리틱스

4. Google 태그 관리자

5. 도메인 이름 공급 업체

인터넷을 검색해본 결과 1번이 가장 보편적이고 간단해 보여서 1번으로 진행하도록 하겠습니다. 

![image](https://user-images.githubusercontent.com/79133602/140528551-7a8e9962-fded-477a-8869-58f0e1c62f46.png)

HTML 파일을 다운 받은 뒤 소유권 확인창을 봤다면 해당파일을 _config.yml 파일과 같은 위치에 넣고 push해줍니다.

![image](https://user-images.githubusercontent.com/79133602/140525266-88091b5a-fb7a-4964-8ab5-c84d384dbdd5.png)

<br/>
<br/>

## 3. sitemap파일 생성



그리고 [xml 생성 사이트](https://www.xml-sitemaps.com/)에 들어가서 검색창에 블로그주소를 입력 후 start를 클릭합니다. 

완성된 xml파일을 다운로드하고 _config.yml이 있는 위치에 넣고 push해주세요.

(저의 경우 jekyll테마에 기본제공되는 sitemap.xml이 있었는데,
또 만들면 에러가 나니 중복을 확인해 주세요. )

만약 config.yml의 **Plugins** 설정에 - jekyll-feed가 주석처리 됐다면 활성화해주세요.


<br/>
<br/>
## 4. robots파일 생성

역시 같은 위치에 위 이름으로 파일을 생성한 뒤 코드를 아래처럼 입력해줍니다.

```
User-agent: *
Allow: /

Sitemap: https://bellasimi.github.io/sitemap.xml
```

Allow에는 사이트 검색시 노출되는 정보에 제한두고 싶은 내용을 입력하시면 됩니다. 


## 5. sitemap파일 등록

![image](https://user-images.githubusercontent.com/79133602/140528952-9367ff7e-bd3a-4bf5-89c8-f2f2383894cb.png)

Google Search Console 속성에 들어가서 sitemaps 메뉴를 클릭, 본인의 url 뒤에 파일명 sitemap.xml을 입력 후 제출을 눌러주세요

![image](https://user-images.githubusercontent.com/79133602/150058102-b2c8e09b-dd23-4441-8de9-5afcf18dee72.png)



그러면 저처럼 알 수 없음이 뜨실텐데요. 

오류가 난게 아니라 처리하는 데 시간이 걸려서 그런거라고 하네요.
빠르면 일주일 내 늦으면 1달까지도 걸린다고 하니... 다른 일을 하면서 기다리시면 좋을 듯 합니다.  😉 


---

> 깃허브 블로그 검색 등록

[네이버,다음 검색 등록](https://bellasimi.github.io/blog/%EB%84%A4%EC%9D%B4%EB%B2%84,%EB%8B%A4%EC%9D%8C-%EA%B2%80%EC%83%89-%EB%93%B1%EB%A1%9D/)

---


<br/>
<br/>
<br/>
# 참고


💻 [https://velog.io/@eona1301/Github-Blog](https://velog.io/@eona1301/Github-Blog-%EA%B2%80%EC%83%89%EC%B0%BD-%EB%85%B8%EC%B6%9C%EC%8B%9C%ED%82%A4%EA%B8%B0)




