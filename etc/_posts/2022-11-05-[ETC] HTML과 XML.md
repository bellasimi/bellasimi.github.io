---
title: "[ETC] HTML과 XML"
categories:
  - html
  - xml
toc: true
toc_sticky: true
---

## HTML

> HyperText Markup Language

HTML은 웹페이지 및 웹 응용 프로그램을 만드는 표준 마크업 언어입니다.

- HyperText : 참조(하이퍼링크)를 통해 다른 문서로 즉시 접근할 수 있는 텍스트
- Markup Language : 태그 등을 이용해 문서나 데이터 구조를 명시하는 언어

<br/>

## XML

> Extensible Markup Language

사람과 기계가 읽을 수 있는 형태로 문서를 인코딩하기 위한 마크업언어로 다른 플랫폼 간 데이터를 교환할 수 있습니다.

- 문서의 구조를 설계 → 해당 규칙으로 내용 예측 가능

```jsx
<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
<book>
<chapter>
	<title>자바스크립트 1장</title>
	<content>내용...</content>
</chapter>
<chapter>
	<title>자바스크립트 2장</title>
	<content>내용2...</content>
</chapter>
</book>
```

<br/>

## 공통점

둘 다 태그로 정보의 계층 구조화한다는 공통점이 있습니다.

<br/>

## 차이점

|                | HTML                                   | XML                                                                  |
| -------------- | -------------------------------------- | -------------------------------------------------------------------- |
| 중점           | 데이터 표시                            | 정보전달                                                             |
| 목적           | 웹페이지 구현                          | 다양한 플랫폼 간 데이터 교환                                         |
| 역할           | 웹페이지 및 응용프로그램의 구조를 만듬 | 사람, 기계 모두 읽을 수 있는 형태로 문서를 인코딩하기 위해 규칙 정의 |
| 대소 문자 구분 | 구분하지 않음                          | 구분                                                                 |
| 태그           | 미리 정의된 태그 존재                  | 프로그래머가 정의                                                    |
| 닫는 태그      | 일부 태그는 존재하지 않음              | 사용된 태그 마다 필요                                                |

XML 역시 태그를 사용하고 있기에 HTML의 태그를 사용하면 HTML 형식의 문서를 만들 수 있습니다. 예로 React의 JSX의 경우, 직접 만드는 컴포넌트 태그와 HTML 태그를 조합해 만드는 형태이기에 XML을 사용해 나타냅니다.
