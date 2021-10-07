<br/>
Prettier란 코드 포멧터(Code Formatter)로 규칙을 작성하면, 코딩 문서를 해당 규칙에 맞는 스타일로 변환해 줍니다. 
<br/><br/><br/>

# 장점

규칙에 맞게 자동으로 정렬이 되기 때문에 가독성이 높아지고 코드 스타일을 통일할 수 있습니다. 
<br/>

# 설정 방법

## 1. IntelliJ IDEA Plugins 설치

![image](https://user-images.githubusercontent.com/79133602/135085213-40dd815a-62c7-4c85-b14c-d568bd7a6ccc.png)

Settings(ctrl+alt+s) - plugins - prettier검색 - install - 인텔리제이 재시작
<br/><br/>

## 2. Dependencies 설치

터미널에서 아래 명령어를 입력해 Dependencies를 설치해줍니다. 
$ npm install --save-dev --save-exact prettier
<br/><br/>

## 3. Prettier 설정

Settings-Languages & Frameworks -JavaScript - Prettier

Node Interpreter : 프로젝트에 사용중인 버전의 node를 선택
Prettier package : 프로젝트 루트 디렉토리/node_modules/prettier 모듈 디렉토리 선택
<br/><br/>

## 4. .prettierrc.jc 파일 생성

예시) css 파일 

# 적용
<br/>

Ctrl + Shift + Alt +P
<br/><br/><br/>

# 참조

💻 <https://prettier.io/>
