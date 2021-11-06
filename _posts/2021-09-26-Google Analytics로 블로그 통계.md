
<br/> <br/>
오늘은 Google Analytics로 사이트 통계를 내는 법을 알아보도록 하겠습니다. 
전체 설명을 하기전,

이미 google anaylitic가 있지만 tracking ID를 모르신 경우엔 [여기로](#2-tracking-id-찾기) 

Tracking ID도 아는 경우엔 [여기로](#3-configyml-수정하기) 가서 글을 읽어주세요! 😎

 
<br/> <br/>
 

# 1. Google Analytics 생성 


먼저 [google analytics](https://analytics.google.com/analytics/web/)에 접속해 주세요 

 
![image](https://user-images.githubusercontent.com/79133602/134811876-80fb26f0-efde-4a04-aec8-e0f3e9d75f34.png)

 
 <br/> 
 

측정시작을 눌러준 다음 계정이름을 지정

 
![image](https://user-images.githubusercontent.com/79133602/134811897-25a23316-bf55-4bf9-a99e-ec4f16cea9e0.png)



속성 설정을 다음과 같이 변경후, <br/> 

 
![image](https://user-images.githubusercontent.com/79133602/134811904-f0878d18-ab54-4995-a830-3a9f6aa37c7a.png)


자신에게 해당되는 체크박스를 선택한 후 만들기를 눌러줍니다. <br/> 

 
![image](https://user-images.githubusercontent.com/79133602/134811926-5ce95e27-baba-4cb6-b314-be4f7d41dad4.png)

 
그리고 구글 애널리틱스에 동의를 눌러주면 완료화면이 나타납니다.<br/><br/>


# 2. tracking ID 찾기 



완료 후 메인 페이지 사이드 메뉴 맨 아래 관리 버튼을 클릭해주면 
 
![image](https://user-images.githubusercontent.com/79133602/134811997-87311f4f-beef-4346-8404-cdbfc5674e7f.png)

 
관리자 화면이 뜨는데 여기서 데이터 스트림 메뉴를 선택해줍니다. <br/> 

 ![image](https://user-images.githubusercontent.com/79133602/134812025-a69d642a-96df-4a58-9e59-7e1a9bba86ef.png)



지금 저 같은 경우는 스트림이 생성이 안됐는데 만약 됐다면 여러분 화면엔 목록이 보일 거에요. 그럼 그 스트림을 클릭하고 나온 웹스트림 세부정보에 측정 ID가 tracking ID입니다.<br/> 

 

만약 저처럼 없다면 

 ![image](https://user-images.githubusercontent.com/79133602/134812049-c7cf5921-6256-4b15-9d39-b3ae6644f18d.png)


웹을 클릭 후 아래와 같이 입력후 스트림 만들기를 해주세요<br/> 

 
![image](https://user-images.githubusercontent.com/79133602/134812055-dd9b9b5d-16e8-4e0a-b085-80a540a4b595.png)

 
그러면 세부정보가 뜨면서 tracking ID를 알아낼 수 있습니다.

 
![image](https://user-images.githubusercontent.com/79133602/134812068-5750cfad-8b80-4bd2-841f-9ae272a0e2c6.png)

 

<br/> <br/>

 

# 3. _config.yml 수정하기 

 

수정파일은 해당 블로그 폴더 내에 있습니다. <br/> 

 

```
# Analytics 

analytics: 

  provider               : false # false (default), "google", "google-universal", "google-gtag", "custom" 

  google: 

    tracking_id          : 

    anonymize_ip         : # true, false (default) 

```

 

위와같은 기본값을 아래처럼 바꿔준 뒤 commit and push를 하면 google analytics가 적용됩니다.  

 

``` 

# Analytics 

analytics: 

  provider               :   "google-gtag" 

  google: 

    tracking_id          : “G-VBDP11HPZL” 

    anonymize_ip         : # true, false (default) 
```

<br/> <br/><br/>
# 참고

💻 [https://velog.io/@eona1301/Github-Blog](https://velog.io/@eona1301/Github-Blog-%EB%B0%A9%EB%AC%B8%EC%9E%90-%ED%86%B5%EA%B3%84Analytics%ED%95%98%EA%B8%B0)