---
title: 
categories:
tags:
- error
- git
last_modified_at:
---

어느날 git을 사용하던 중 다음과 같은 에러메세지를 만났습니다. 
```
fatal: Unable to create '레포지토리로컬경로/index.lock': File exists. Another git process seems to be running in this repository, e.g. an editor opened by 'git commit'. Please make sure all processes are terminated then try again. If it still fails, a git process may have crashed in this repository earlier: remove the file manually to continue.
ㅣ
```
<br/>
# 원인

저같은 경우엔 add .를 한다음 git commit -m 대신 git commit -a(얘는 add와 commit을 함께 처리해줌)해서 충돌이 났었네요 😅

![image](https://user-images.githubusercontent.com/79133602/133926346-40f228ec-6a9e-441b-9102-fe9c574aa0dc.png)

아까 콘솔이 먹통이 되서 중간에 git을 강제 종료 했을때 

![image](https://user-images.githubusercontent.com/79133602/133926361-dc042a1d-ed02-46ec-bd4f-adfcca00eac9.png)

이런 메세지가 떴는데 그 처리과정이 여전히 진행중인 것 같아요.

<br/><br/>
# 해결

![image](https://user-images.githubusercontent.com/79133602/133926062-a713f275-79bf-47c2-a644-17ce6a28ae30.png)

터미널에 다음과 같이 입력해주세요.
```
rm -f ./.git/index.lock
```

<br/>
# ❗ 주의

 저같은 경우 해당 폴더위치에서 저 명령어를 쓰면 해결되지 않고 상위 폴더에서 썼을 때 해결됐습니다. 아마 처음 로컬 레포지토리 위치에 index.lock 파일이 생성되나 보더라구요.


<br/>
<br/>
# 참고

💻 <https://goddaehee.tistory.com/220>