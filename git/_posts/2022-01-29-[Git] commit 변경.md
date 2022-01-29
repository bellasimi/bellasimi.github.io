---
title: 
categories:
tags:
- git
last_modified_at:
---

만약 commit시 메세지를 잘못 입력했다면 아래 방법으로 수정하시면 됩니다.

<br/>
## 방금 전에 한 commit인 경우

```
git commit --amend
```

터미널에서 git commit --amend라고 명령합니다.

![image](https://user-images.githubusercontent.com/79133602/151664326-366da588-7578-41de-bf69-24ce9e5fe969.png)



그리고 위와 같은 창이 뜨면 노란색 메시지 부분을 바꿔주시고 -esc -:wq를 차례대로 입력해 빠져나오시면 됩니다. 

<br/><br/>
## 훨씬 이전의 commit인 경우

```
git reabse -i HEAD~불러올 commit개수
```

rebase는 branch의 base를 다시 설정해 기존 브랜치와 merge commit생성을 방지해줍니다. 여기에 -i를 붙이면 rebase 명령을 대화형으로 수행해, commit들의 순서를 바꾸거나 commit 내역을 변경, 삭제할 때 사용합니다. 

HEAD는 이전 작업을 의미하고 이 뒤에 ~숫자를 붙이면 해당 숫자 만큼 이전 commit내역을 불러와 수정 수 있습니다. 

```
pcik commit번호 commit메세지

```

형식인데 pick을 reword로 바꾸고 :wq를 입력하면 
해당 commit의 페이지가 뜨는데 여기서 commit 메세지를 바꿔주시면 됩니다. 
그리고 :wq 하시면 입력한 commit 메세지로 수정됩니다. 

<br/><br/>
## 번외: commit 삭제하고 싶을 때

```
git reset HEAD^ //최신 commit 보다 전으로 reset
git reset HEAD^^ //전전으로 reset
```

HEAD는 가장 최신 commit을 의미합니다. HEAD에 ^를 붙이면 최신 commit전이므로 reset하면 현재 commit이 사라지고 그 이전 상태로 reset 됩니다.. ^을 붙이는 갯수로 얼마나 전인지 설정할 수 있습니다. 

<br/>
# ❗ 주의: push한 commit일 때

<br/>
왠만하면 commit을 삭제하지 마세요 ….😫

삭제 후 git push -f origin main을 해야되는데… 그러면 협업중이던 팀 파일들이 변경되고 작업중이던 팀원들이 push하려고할 때 충돌이 일어납니다…. 

<br/><br/><br/>
# 참고

💻 [git 튜토리얼](https://backlog.com/git-tutorial/kr/stepup/stepup7_1.html)
