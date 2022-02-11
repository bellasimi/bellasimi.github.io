---
title: 
tags:
- idol_collector
last_modified_at:
---

다른 분이 백엔드를 개발한 뒤 프론트엔드 작업을 하게됐는데 다음과 같은 오류를 만났다. 	
	
<br/>
## 오류 1 ) 개발자서버 작동 에러

## 원인과 해결

1.  sdk 버전 차이 난 sdk8 - 팀 sdk 11 

build.gradle 8행 수정 11 → 8

`sourceCompatibility = '8'` 이제 11다운 받아서 11로 바꿔놓음

2. jdk 1.8 지원하지 않는 api  Optional 클래스의 isEmpty 존재(jdk 11엔 있나보네)
    
    전
    
     `if(opt.isEmpyt())` 
    
    후
    
    `if(!opt.isPresent())`
    
3. oauth2 계정 없다
    
    main 환경설정 application.properties에 추가, 백엔드 개발자분은 test로만 돌리고 계신 모양
    
    ```
    spring.profiles.include=dev
    
    # Social login
    #google
    spring.security.oauth2.client.registration.google.client-id= 898772596258-uqpr9bb34p9dt5i51jbjcm49k2abdm72.apps.googleusercontent.com
    spring.security.oauth2.client.registration.google.client-secret= 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
    spring.security.oauth2.client.registration.google.scope= profile,email
    ```
    
    test application.properties엔 있는데 main엔 없었음
    
4. 파일 경로 el식 이해 못해
    
    FileStore 클래스에서 ${file.dir} 못 가져옴
    
    그래서 아래 경로
    
    `file.dir=./src/test/resources/imgs/`
    
    직접 넣음
    
    ```
    public class FileStore {
    
        @Value("./src/test/resources/imgs/")
        private String fileDir;
    ```
    
5. port 8080 사용중

main application.properties에 다음 추가 

`server.port = 8001` 

이거 싫으면 cmd > netstat -a -o > port의 pid 찾아서 taskkill/f /pid pid번호

<br/>
## 오류2 ) 구글 로그인 오류

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed759515-eb31-4435-ae8e-304b47700975/Untitled.png)

구글 로그인 api에서 관리자가 redirect_uri를 [http://localhost:8080/](http://localhost:8080/)으로 설정해뒀는데 내가 server.port를 8001로 바꿔서 생긴 오류