# IntelliJ가 실행이 안될 때
cmd 창에 cd 인텔리제이가 있는 파일 주소명을 입력 - idea.bat을 입력해줍니다.
그랬을 때 다음과 같은 메세지가 뜬다면
![캡처1](https://user-images.githubusercontent.com/79133602/133450360-9bc07df4-53c9-466e-a3c3-ab91b6f3f093.PNG)

문제가 있는겁니다 👿

저같은 경우엔 VMoptrions file에 한글 인코딩을 하다가 오타가 나서 
-Dfile.encoding = UTF- 8 라고 써야될 걸 -Dfile.encoding = UTF=8라고 써서 이런 오류가 난거 같은데

정작 VMoptions 파일을 해당디렉토리에 가서 직접 열어보니 ... 
😱😱

한글 인코딩 부분자체가 저장이 안돼있더라구요.
그럼 도대체 저 오타는 어디에 저장이 됐고 어떻게 복구를 시키나...
 
밑에는 해결과정이 다 써져 있기에 
결과만 보고 싶으신 분은 [해결법](#5-사용자-appdata에-있는-jetbrain-폴더-삭제) 클릭해주세요!

# 1. 재설치

기존 인텔리제이를 삭제하고 재설치를 해봤지만 여전히 같은 에러 메세지가 뜨더군요.

# 2. 시스템 복구 

![image](https://user-images.githubusercontent.com/79133602/133452704-8baa0642-dcc1-4a4c-be11-7de698fe86b9.png)

내PC 우클릭 - 속성 - 시스템 메뉴 중 좌측 시스템 보호 - 시스템 복원 - 저런 오류가 발생하기 전 시점으로 복구

결과는.... 😭 여전히 같은 오류.. 

# 3. 구글링 및 커뮤니티에 질문

스택오버플로우나 오키같은 사이트에 물었으나 VMoptions 파일에 해당 오타를 지우라는 답만 들었습니다. 
하지만 제 VMoptions 파일은 아래와 같이 오타는 커녕 한글 인코딩 부분 조차 존재하지 않습니다. 

![ex -vmoptions](https://user-images.githubusercontent.com/79133602/133453546-2e67903e-1114-4838-af21-49c61d979b2d.PNG)

# 4. JetBrain에 직접 문의 
![image](https://user-images.githubusercontent.com/79133602/133453808-3ab5afa1-d88b-46db-904c-2cccf1645eb2.png)
여전히 VMoptions파일을 지우라는 말뿐입니다. 

앞으로 해결을 해야될텐데... 일단 저 답변에 그렇게 했는데도 안되고 제 디렉토리 상태와 오류 메세지 오류가 발생한 원인에 대해 더 적어뒀는데 제발 해답을 알려주길 바랄 뿐입니다.


# 5. 사용자 AppData에 있는 JetBrain 폴더 삭제
먼저 AppData를 보기 위해 탐색기의 보기 메뉴에서 숨긴항목 보기를 체크해줍니다.

![image](https://user-images.githubusercontent.com/79133602/133564367-a5514c14-4b9b-48ed-b5e3-e8d26510a58f.png)

그다음 사용자 폴더로 들어가면 (보통 내PC -C - 사용자 -사용자명으로 들어가면된다.) 전에 안보이던 AppData가 보이는 걸 알 수 있죠!!

![image](https://user-images.githubusercontent.com/79133602/133564686-3744e500-c602-4086-a561-82a418149abe.png)

해당 폴더 안엔 다음과 같은 폴더가 있는데 검색창에 JetBrains를 치거나 또는 

![image](https://user-images.githubusercontent.com/79133602/133563553-38665ee6-da33-4616-94a1-c7c53c876214.png)

그냥 Roaming, Local 폴더에 들어가서 JetBrains 폴더를 찾아 삭제해주면됩니다. 

![image](https://user-images.githubusercontent.com/79133602/133563726-ac50d7ca-d151-4b95-b4ac-ff3d99903b12.png)

그다음 IntelliJ를 삭제해 주고 재설치하면

![image](https://user-images.githubusercontent.com/79133602/133561844-4177b42c-a2c4-407f-bc57-90d2ced717c4.png)

다시 정상작동하는 것을 볼수 있습니다!!😆


<참고>

'인텔리제이 공식 홈페이지' : <https://intellij-support.jetbrains.com/hc/en-us/articles/360007568559>
