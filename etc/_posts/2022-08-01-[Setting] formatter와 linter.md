---
title: "[Setting] formatter와 linter"
categories:
  - etc
tags:
  - formatter
  - linter
  - prettier
  - eslint
  - setting
toc: true
toc_sticky: true
---

![image](https://user-images.githubusercontent.com/79133602/189559330-a8980639-0d77-4659-82ae-7e2ca71924f6.png)

<br/>

# formatter 와 linter란?

> **formatter:** 스타일 , **linter:** 문법

코딩을 외국어라고 치고, formatter의 역할을 분리해보자면 style formatter는 발음, 추임새를 교정해 주는 선생님 linter는 문장 및 문법을 교정해주는 선생님이라고 할 수 있습니다.

다시말해서, **스타일을 교정**하는 데는 **prettier 포맷터**를 사용하고, **코드를 정해 둔 규칙**대로 구현했는지 **오류를 파악**할 때는 **eslint**를 사용하면 됩니다.

<br/>

## 대표적인 라이브러리

> **prettier:** formatter + **Eslint:** linter

대표적인 formatter, linter 라이브러리로는 각각 prettier, eslint가 있습니다. npm이나 yarn을 통해 설치하고 json, js파일에 설정값을 작성하면 해당 설정값으로 코드 스타일이 수정됩니다.

<br/>

### 사용 방법

1. 라이브러리 설치

   ```jsx
   npm i -D eslint prettier // 리액트 CRA의 경우 eslint가 자동 설치된다.
   ```

2. eslint, prettier **vscode extention을 설치**

<br/>

## 좋은 format, linter 규칙이란 뭘까

스타일의 경우 주관이 강하게 반영됩니다. 그래서 설득을 하기 힘들고 대부분 다수결로 결정이 될 수 밖에 없습니다. 예로 prettier semi를 붙이는 규칙은 문제가 발생하는 부분도 아니고 단순히 세미콜론이 보기 좋냐 아니냐의 취향차입니다.

반면 eslint는 좀 더 객관적인 이유로 선택이 가능합니다. 조건문에서 한줄인 경우 {}를 빼면 발생 가능한 오류가 있으니 미연에 방지하기 위해 {}를 강제한다던지, 식별자 중복을 막기위해 선언된 식별자가 재사용되면 에러가 뜬다던지 하는 예가 그렇습니다. 하지만 에어비앤비룰처럼 너무 강경한 경우 에러가 많이 뜨고, 해당 에러 코드를 수정하는 데 시간을 많이 뺐기기 때문에 초심자라면 무리해서 사용하지 않는 게 좋습니다.

<br/>

## endofLine을 통일하는 게 중요

그럼에도 불구하고 객관적으로 필요한 스타일 규칙도 있습니다. endofLine의 경우 운영체제마다 줄바꿈 방식이 다른데( 윈도우는 CRLF, 맥은 LF) auto로 해두면 자기 운영체제의 방식을 쓰게 됩니다. 문제는 GIT이 줄바꿈방식까지 diff로 잡아낸다는 점이다. 즉, 팀원들의 운영체제가 다르면 현재 공유하는 브랜치의 HEAD와 내 파일의 내용이 같을 때도 diff가 뜰 수 있다. 이를 막기 위해선 lf로 통일을 할 필요가 있고 결국 2.0v부터 lf가 프리티어의 기본값이 됐습니다.

<br/><br/>

# formatter 와 linter 간 충돌

prettier와 eslint 모두 **style에 대한 rule**이 있는 경우, 그리고 두 rule이 **다른 경우 충돌**이 발생할 수 있습니다. 그런 경우 추가 설정으로 해결을 해야 합니다.

- **CRA의 기본 eslint는 prettier와 충돌이 없다? ( 아니다 충돌난다! )**
  사실 리액트 CRA에서 기본 제공하는 eslint는 non-style rule만 갖고 있어서 prettier와 충돌은 없지만, 그 외의 경우라면 아래 방법으로 해결해야 합니다.

<br/>

## 충돌 해결 방법

> **eslint-config-prettier 라이브러리 사용**

1.  일단 style을 정하는 건 prettier이기 때문에 vscode setting에서 **prettier를 기본 formatter로 설정**합니다.

    ```jsx
    {
      "editor.formatOnSave": true,
      "editor.defaultFormatter": "esbenp.prettier-vscode",
    }
    ```

2.  충돌을 방지하기 위해 **eslint-config-prettier 라이브러리를 설치**합니다.
    - **eslint-config-prettier:** eslint에서 prettier와 충돌하는 rule를 꺼주는 라이브러리
      ```jsx
      npm i -D eslint-config-prettier
      ```
3.  그리고 **.eslintrc 파일의 extents에 prettier를 추가**합니다.

    ```jsx
    "extends": ["eslint:recommended", "prettier"],
    ```

<br/>

## 번외 : 충돌 방지 다른 방법들

> 비추

### 1. eslint-plugin-prettier

prettier를 eslint의 rule로 작동하도록 만드는 라이브러리입니다. 이러면 포맷팅 문제도 eslint의 오류로 표시되기 때문에 prettier는 스타일 포맷터, eslint는 오류 교정기로 나눠 사용하려는 취지에 맞지 않습니다. 또 eslint 오류 메세지가 많아지는 만큼 느려진다는 단점이 있습니다.

### 2. prettier-eslint

prettier 실행후 eslint —fix를 실행하는 방법입니다. 하지만, 직렬로 작동해서 느리고, 메인테이너도 비추했으니 사용하지 않는 게 좋습니다.

<br/><br/>

# 사용예시

## setting.json

```
  "editor.defaultFormatter": "esbenp.prettier-vscode", // prettier를 기본 포맷터로
  "editor.formatOnSave": true, // 저장 시 자동 포맷팅
  "editor.codeActionsOnSave": { // 저장 시 eslint 적용
    "source.fixAll.eslint": true
  },
  "eslint.codeAction.showDocumentation": { // eslint 메세지에 해당 문서 링크 나오도록
    "enable": true
  }
```

## .prettier.json

```
{
  "arrowParens": "avoid", // 화살표 함수 괄호 사용 방식 - always 기본, 매개변수 추가시 용이함
  "bracketSpacing": false, // 객체 리터럴에서 괄호에 공백 삽입 여부
  "endOfLine": "auto", // EoF 방식, OS별로 처리 방식이 다름
  "htmlWhitespaceSensitivity": "css", // HTML 공백 감도 설정
  "jsxBracketSameLine": false, // JSX의 마지막 >를 다음 줄로 내릴지 여부
  "jsxSingleQuote": false, // JSX에 singe 쿼테이션 사용 여부
  "printWidth": 80, //  줄 바꿈 할 폭 길이
  "proseWrap": "preserve", // markdown 텍스트의 줄바꿈 방식 (v1.8.2)
  "quoteProps": "as-needed" // 객체 속성에 쿼테이션 적용 방식
  "semi": true, // 세미콜론 사용 여부
  "singleQuote": true, // single 쿼테이션 사용 여부
  "tabWidth": 2, // 탭 너비
  "trailingComma": "all", // 여러 줄을 사용할 때, 후행 콤마 사용 방식
  "useTabs": false, // 탭 사용 여부
  "vueIndentScriptAndStyle": true, // Vue 파일의 script와 style 태그의 들여쓰기 여부 (v1.19.0)
  "parser": '', // 사용할 parser를 지정, 자동으로 지정됨
  "filepath": '', // parser를 유추할 수 있는 파일을 지정
  "rangeStart": 0, // 포맷팅을 부분 적용할 파일의 시작 라인 지정
  "rangeEnd": Infinity, // 포맷팅 부분 적용할 파일의 끝 라인 지정,
  "requirePragma": false, // 파일 상단에 미리 정의된 주석을 작성하고 Pragma로 포맷팅 사용 여부 지정 (v1.8.0)
  "insertPragma": false, // 미리 정의된 @format marker의 사용 여부 (v1.8.0)
  "overrides": [
  {
  "files": "*.json",
  "options": {
  "printWidth": 200
  }
  }
  ], // 특정 파일별로 옵션을 다르게 지정함, ESLint 방식 사용
}
```

## .eslintrc.json

```
{
  "env": {
    "browser": true,
    "node": true,
    "es2021": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:react/jsx-runtime",
    "prettier"
  ],
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 2020,
    "sourceType": "module"
  },
  "plugins": ["react", "react-hooks"],
  "rules": {
    "curly": "error",
    "prefer-const": "warn",
    "no-console": "warn",
    "no-unused-vars": "warn",
    "no-shadow": [
      "warn",
      {
        "ignoreOnInitialization": true
      }
    ],
    "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
    "react/prop-types": "warn",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "react/jsx-no-constructed-context-values": "warn",
    "react/jsx-props-no-spreading": "off",
    "react/function-component-definition": [
      2,
      {
        "namedComponents": [
          "function-declaration",
          "function-expression",
          "arrow-function"
        ],
        "unnamedComponents": ["arrow-function"]
      }
    ]
  }
}
```

<br/><br/><br/>

# 참고

💻 [prettier와 eslint를 구분해서 사용하자](https://velog.io/@yrnana/prettier%EC%99%80-eslint%EB%A5%BC-%EA%B5%AC%EB%B6%84%ED%95%B4%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90#prettier%EC%99%80-eslint%EB%A5%BC-%EA%B0%99%EC%9D%B4-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

💻 [ESLint, Prettier 적용하기](https://velog.io/@recordboy/ESLint-Prettier-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0#%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90-eslint%EC%99%80-prettier-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)

- 2번 째 참고 방식 사용 시 npm install eslint-plugin-react-hooks --save-dev를 해야 함

💻 [LF와 CRLF의 차이 (Feat. Prettier)](https://velog.io/@jakeseo_me/LF%EC%99%80-CRLF%EC%9D%98-%EC%B0%A8%EC%9D%B4-Feat.-Prettier)
