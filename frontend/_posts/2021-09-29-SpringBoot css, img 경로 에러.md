
![image](https://user-images.githubusercontent.com/79133602/135301483-cc8454a9-37af-4741-8ad6-0861ad9c883a.png)

프론트 엔드 개발을 하던중 평소에 IntelliJ에서 직접 html로 띄웠을 땐 잘 되던 css와 img가 서버에선 갑자기 전부 깨지는 에러를 겪었습니다. 😱
<br/>

왜 이런일이 발생한 걸까요?
<br/><br/><br/>

# 원인

바로 경로가 잘못 설정했기 때문입니다. 

springboot에선 아래와 같은 폴더명들이 기본경로로 지정돼있어서 

![image](https://user-images.githubusercontent.com/79133602/135304257-d6f98ae8-eff2-472a-8578-f96dc6816aba.png)

그 안의 파일들을 자동으로 인식합니다. 즉, /static을 아래처럼 경로에 쓰면 중복이 됩니다. 

![image](https://user-images.githubusercontent.com/79133602/135302928-3a203a05-72de-4461-abfb-c57f6a11c368.png)
<br/><br/><br/>

# 해결법

위의 경로를 아래와 같이 /static을 빼고 입력해줘야 됩니다. 

![image](https://user-images.githubusercontent.com/79133602/135302820-7a85a80b-7af9-41d8-96e3-49afa797f1c7.png)

그러면  local:8080 springboot 서버로 돌렸을 때 css와 img가 잘 나오는 것을 볼 수 있습니다. 

![image](https://user-images.githubusercontent.com/79133602/135301843-9c3b3466-0639-489c-8913-6fdb846fb64c.png)

<br/><br/>
다만 그냥 html을 인터넷 페이지로 열어볼 땐 스프링 부트를 사용하는 게 아니라서 /static이 필요하니 혹시 frontend 작업을 확인할 땐 써주시고 나중에 ctrl+shift+r을 눌러서 변경해주세요(IntelliJ 기준입니다.)

<br/><br/><br/>
# 참조

💻 <https://spring.io/blog/2013/12/19/serving-static-web-content-with-spring-boot>
