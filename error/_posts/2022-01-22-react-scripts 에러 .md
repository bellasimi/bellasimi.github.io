---
title: 
categories:
- react
tags:
- react
- error
last_modified_at:
---


> 'react-scripts'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다. 

평소처럼 npm start로 리액트 프로그램을 실행하려는데 위와 같은 오류를 만났습니다. 😫 

원인은 무엇이고 어떻게 해결해야 할까요?
<br/><br/>
# ❓ 원인

해당 프로그램 경로에 react-scripts 모듈이 제대로 설치되지 않았거나 버전이 구형이라 발생한 오류입니다.
<br/><br/>
# ❗ 해결 방법

> yarn upgrade

버전이 구형이라면 yarn add upgrade를 해주시면 됩니다. 만약 react-scripts 모듈이 제대로 설치되지 않은 경우라면 
다음 명령어 중 하나를 택해 터미널에 입력해주세요.

> yarn add react-scripts

> npm install -save react-scripts

<br/><br/>
# 번외

> yarn add global react-scripts

전역설치를 하면 require함수나 경로를 길게 쓰지 않고 패키지를 사용할 수 있는데요. react-scripts는 굳이 그럴 필요 없습니다.

> yarn remove global react-script

만약 실수로 전역 설치하신경우 위 명령어를 입력시 삭제 가능합니다.