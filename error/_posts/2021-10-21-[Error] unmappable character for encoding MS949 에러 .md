---
title: 
categories:
tags:
- error
last_modified_at:
---


오늘 만난 에러는 다음과 같습니다. 

![image](https://user-images.githubusercontent.com/79133602/138111880-8ff1e3d7-5ccc-44a2-84a7-02b9fae5fe88.png)


<br/>
# 원인 🤔

사용자가 입력한 문자나 기호를 컴퓨터가 이해할 수 있는 신호로 바꿔주는 작업을 인코딩이라고 하는데요. 

윈도우의 기본 인코딩은 MS949라서 한글을 인식하지 못합니다. 그래서 따로 UTF-8인코딩을 해주지 않은 경우 위와같은 오류가 발생합니다. 

이를 고치기 위해선 다음과 같은 일을 해야합니다. 




<br/><br/>
# 파일 인코딩

인텔리제이 기준 

<br/>
##  File - Settings - Editor - File Encodings 

위 메뉴에 들어가서  다음과 같이 설정을 변경해줍니다. 

![image](https://user-images.githubusercontent.com/79133602/138114032-d62dbee3-91dd-4050-9f65-93939caf5fd5.png)

적용을 누르고 실행해주세요.

만약 저처럼 한글이 깨져서 나올 경우 한글 VMpotions 파일에 한글인코딩을 입력해줘야합니다. 

![image](https://user-images.githubusercontent.com/79133602/138114402-cf70cba7-85cd-4b7e-b698-983cafdfd727.png)

[VMoptions설정 변경](https://bellasimi.github.io/intelliJ-%ED%95%9C%EA%B8%80-%EA%B9%A8%EC%A7%90-%EC%9D%B8%EC%BD%94%EB%94%A9/)



<br/><br/><br/>
# 참조

💻 [인텔리제이 공식사이트](https://www.jetbrains.com/help/idea/2019.2/configuring-individual-file-encoding.html#console)