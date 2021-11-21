---
layout: post
title: HTML, XML과 JSON 차이
category: CS
tags: [CS]
comments: true
---
<br>
<p align="center"><img width="80%" src="https://user-images.githubusercontent.com/76654131/142766400-f6d320dd-b396-425d-ba35-f7999eb25fd4.png"></p>


### HTML(HyperText Markup Language)

- 웹페이지에 데이터를 표현하기 위한 마크업 언어

### XML(EXtensible Markup Language)

- 데이터를 저장과 전송을 목적으로 만들어진 마크업 언어

---

## HTML과  XML의 차이

### 1. 목적성

**HTML**이 데이터의 표현에 목적을 두고 있다면,  **XML**은 데이터 교환을 위한 구조 정의에 목적을 두고 있다.

### 2. HTML 태그는 미리 정해져 있다면,  XML은 사용자가 직접 태그 정의 가능

```html
// HTML
<html>
  <head>
    <title>제목입니다</title>
  </head>
  <body> 
    <h1>H1 텍스트입니다.</h1>
    <p>P 텍스트입니다.</p> 
  </body> 
</html>
```

\* HTML에서는 html태그 head태그 body태그 등 미리 정해진 태그가 그 의미에 맞게 사용되고 있다.              
```xml
// XML
<title>제목입니다</title>
<content>내용입니다</content>
<sender>발송자</sender>
```

\* XML태그는 사용자가 입맛대로 직접 태그명을 만들어 필요에 맞춰 사용한다. 즉, XML은 미리 정의된 태그가 없다.

### 3. 환경

HTML이 인터넷 웹환경에서만 작동되는 언어라면,  XML은 특정 환경에 구애 받지 않는다.

- HTML = 웹 브라우저 환경에서만 실행 가능
- XML = 다목적 마크업 언어답게 특정 애플리케이션에 종속되지 않고 사용 가능

### 4. 표현의 유무

HTML은  데이터를 웹브라우저 환경에서 표현하고 나타낼 수 있지만,   
XML은 태생이 데이터를 저장하고 전달하기 위한 언어이기 때문에 데이터를 가지고 있을 뿐,  표현하진 않는다.

---

## XML과  JSON

**웹에서 API로 통신을 할 때 데이터를 전달받는 형식이 있다.**

**그 형식인 XML**과 **JSON**은 _HTML_처럼 데이터를 보여주는 목적이 아닌, **데이터를 저장하고 전달할 목적**으로만 만들어졌다.

🔎 **잠깐 보는 XML과 JSON의 추가 공통점**

XML과 JSON은 기계뿐만 아니라 사람도 쉽게 읽을 수 있으며, 다양한 프로그래밍 언어에 의해 파싱될 수 있다.   
그리고 둘다 **XMLHttpRequest 객체**를 이용하여 서버로부터 데이터를 전송 받는다.

<p align="center"><img width="80%" src="https://user-images.githubusercontent.com/76654131/142766609-4beacc12-0990-46aa-90d0-5720f79e06d2.png"></p>

## XML(EXtensible Markup Language)

-   문서의 구조 정보를 표현하기 어려운 HTML의 한계를 극복하기 위한 다목적 마크업 언어로 **태그** 등을 이용하여 데이터의 구조를 기술하는 언어다.  

## XML 특징

-   데이터에 의미를 부여하는 **메타데이터**를 선언할 수 있다. (XML의 탄생 목적)
-   XML은 단순히 정보 전송이 아니고 **정보의 의미를 표현**하는 데 있어 큰 이점

```xml
<dog>
    <name>식빵</name>
    <family>웰시코기<family>
    <age>1</age>
    <weight>2.14</weight>
</dog>
```
실제 강아지 데이터는 식빵, 웰시코기, 1, 2.14 이며, <dog> <name> <family> 등이 실제 데이터가 무엇을 의미하는지 나타내는 메타 데이터이다.   
XML은 메타 데이터를 표현하는 마크(태그)를 확장할 수 있어서 어떠한 데이터도 표현할 수 있다.

---

## JSON(JavaScript Object Notation)

-   데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 DATA 교환 형식**  
-   Javascript에서 객체를 만들 때 사용하는 표현식을 의미
-   JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다
-   JSON은 데이터 포맷일 뿐이며 어떠한 통신 방법도, 프로그래밍 문법도 아닌 단순히 데이터를 표시하는 표현 방법일 뿐이다.

## JSON 특징

-   서버와 클라이언트 간의 교류에서 일반적으로 많이 사용된다.
-   자바스크립트 객체 표기법(key와 value가 한 쌍을 이루는)과 아주 유사하다.
-   자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있다.  
    -   **JSON.parse( JSON으로 변환할 문자열 )** : JSON 형식의 텍스트를 자바스크립트 객체로 변환한다.
    -   **JSON.stringify( JSON 문자열로 변환할 값 )** : 자바스크립트 객체를 JSON 텍스트로 변환한다.
-   **JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어졌다.**
-   자바스크립트의 문법과 굉장히 유사하지만 **텍스트 형식일 뿐**이다.
-   다른 프로그래밍 언어를 이용해서도 쉽게 만들 수 있다.
-   특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다.

 위에 XML 예제를 JSON 형태의 데이터로 바꾸면 다음과 같다.

```json
// key-value 형식의 쌍
{
    "name": "식빵",
    "family": "웰시코기",
    "age": 1,
    "weight": 2.14

// 값들의 순서화된 리스트 형식 (배열 가능)
    "hobby": ["sleeping","swimming"]
}
```

---

## XML과 JSON의 차이

<p align="center"><img width="80%" src="https://user-images.githubusercontent.com/76654131/142766754-d5ab7241-cc59-4a0c-aaf0-c12836b0a46a.png">
</p>


---
<br>
JSON을 많이 쓰는 추세지만 XML이 사라지지 않는 이유가 있다.

지금은 정확히 모르겠지만 XML만의 수치 외적인 강점이 있기 때문이란다.

나중에 프로젝트를 설계하고 개발할 때  XML과 JSON의 사용에 대해 고민해보고 적절하게 사용하는 개발자가 되야겠다.

참고링크) [**왜 여전히 XML 사용을 고려해야 하는가?**](https://www.coovil.net/xml-vs-json/)

<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://www.crocus.co.kr/1493](https://www.crocus.co.kr/1493)   
[http://tcpschool.com/json/json_intro_xml](http://tcpschool.com/json/json_intro_xml)   
[https://velog.io/@surim014/JSON이란-무엇인가](https://velog.io/@surim014/JSON이란-무엇인가)