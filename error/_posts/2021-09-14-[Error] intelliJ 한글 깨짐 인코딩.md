---
title: 
categories:
tags:
- error
- intellij
last_modified_at:
---

IntelliJ로 작업을 하다가 console창에 한글이 깨져 나오거나

![image](https://user-images.githubusercontent.com/79133602/133250990-4cb79cf6-59b9-4dad-ad67-6ec92e13a795.png)

작업하는 html파일을 IntelliJ를 통해 바로 인터넷창에 띄웠는데 깨져 나온다면

![image](https://user-images.githubusercontent.com/79133602/133251194-2f1a9aa7-8e32-4577-9a4a-2ad6c185d976.png)

![image](https://user-images.githubusercontent.com/79133602/133251412-e8c6effd-a217-4b02-943a-532c62cf2c68.png)

인텔리제이 한글 인코딩이 안됐기 때문입니다.

<br/>
#해결법


# 1. IntelliJ VM 설정변경

IntelliJ 실행 후 help - edit custom VM Options에 들어가서 맨 아랫줄에 다음과 같이 입력해주세요

![image](https://user-images.githubusercontent.com/79133602/133567824-b30b2bf5-df85-4359-85e3-0d22791e10eb.png)

```
-Dfile.encoding=UTF-8
-Dconsole.encoding=UTF-8
```

오타가 나거나 띄어쓰지 않도록 주의!

<br/>
# 2. IntelliJ Editor File Encoding

> file - settings - editor - file encodings 

해당 디렉토리에 들어가서 아래와 같이 설정을 변경해 줍니다.

![image](https://user-images.githubusercontent.com/79133602/133252230-ba8fa7a6-072d-44f5-9d2d-dba89dbb3970.png)

<br/>
# ✔ Transparent native-toascii conversion 체크박스는 property 파일의 유니코드값으로 표현돼 있는 한글을 원본으로 보여줄지를 선택합니다.

<br/>
# 3. 톰캣 인코딩 설정 

상단메뉴 Run - edit configurations -VM options에 다음을 추가해 줍니다.

```
-Dfile.encoding=UTF-8

```

<br/>
# 4. 그래도 안되면... 

프로젝트의 build 파일 우클릭 clean -rebuild를 해주세요! 