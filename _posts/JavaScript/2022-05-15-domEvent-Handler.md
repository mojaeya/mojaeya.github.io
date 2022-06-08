---
layout: post
title: DOM 이벤트와 이벤트 핸들러 개념
category: JavaScript
tags: [javascript, dom]
comments: true
---

## DOM 이벤트(Event)

웹 페이지를 이용하면 웹 화면과 사용자 사이에서 수많은 상호작용이 나타난다.
버튼을 클릭한다든지, 마우스로 스크롤, 검색 키워드를 입력하는 행동 등 이렇게 사용자가 웹 페이지를 이용하면서 행하는 액션을 `이벤트(Event)`라고 한다.

`이벤트(Event)`가 발생하면 보통 사전에 정의된 특정 코드가 실행되고 그에 따라 기능이 동작하거나 화면이 변경되는 등의 변화가 발생 한다.

---

## 이벤트 핸들러(Event Handler)

`이벤트 핸들러`는 이벤트 발생을 감지하고 처리할 코드를 수행하는 역할을 한다.

<font color='red'>이벤트 핸들러는 앞의 이벤트 이름 앞에 on을 붙여 사용한다.</font>

<br>

#### 이벤트 처리의 방법

`예시 : click 이벤트`

#### 1. HTML 태그의 속성으로 정의하는 형식

```html
<body>
  <button onclick="myFunction();">클릭</button>
</body>

<script>
  function myFunction() {
    console.log("onclick 이벤트 발생");
  }
</script>
```

#### 2. 자바스크립트에서 DOM 엘리먼트의 속성에 콜백 함수를 정의하는 형식

```html
<body>
  <button id="btn">클릭</button>
</body>

<script>
  document.getElementById("btn").onclick = function () {
    console.log("콜백함수 정의");
  };
</script>
```

#### 3. <font color='red'>addEventHandler()</font>를 이용한 이벤트 핸들러를 추가하는 형식

이벤트 요소를 추가하기 위한 가장 구조적인 방법으로 onclick 속성에 콜백 함수를 구현하는 것 보다 좋은 방법.

```html
<body>
  <button id="btn2">클릭</button>
</body>

<script>
  document.querySelector("#btn2").addEventListener("click", function () {
    console.log("이벤트 리스너 사용");
  });
</script>
```

---

#### 📌 가장 나은 방법은 3번 `addEventHandler()`를 이용한 이벤트 핸들러를 추가하는 방법이다.

1번처럼 `HTML 태그에 직접 이벤트가 달려있으면` 예를 들어 나중에 퍼블리셔나 웹디자이너분들이 화면 변경을 하거나, 구조를 바꾸는 경우 다시 일일이 새로 받은 HTML에 이벤트를 다시 걸어줘야하는 <font color='red'>번거로운</font> 경우가 발생한다.

하지만 3번처럼 `자바스크립트 안에서 따로 이벤트 관리`를 하고 있다면, 화면이 많이 변경이 된다고 해도 새로운 HTML 태그에 이벤트를 달아주는 <font color='#1E90FF'>불필요한 작업이 필요없게 된다.</font>

그리고 `자바스크립트 안에서 따로 이벤트 관리`를 하는게 <font color='red'>태그안에서 이벤트들이 뿔뿔히 흩어져 있는 것 보다</font> <font color='#1E90FF'>가독성 면에서도 훨씬 좋고 관리하기 편하다.</font>

```html
<body>
  <button id="btnSave">저장</button>
  <button id="btnSearch">조회</button>
  <button id="btnDelete">삭제</button>
</body>

<script>
  // 가독성있게 관리하기 위해서 setEvent 함수안에 이벤트 수행 코드들을 모아놓고
  function setEvent() {
    document.getElementById("btnSave").addEventListener("click", function () {
      console.log("저장 실행");
    });

    document.getElementById("btnSearch").addEventListener("click", function () {
      console.log("조회 실행");
    });

    document.getElementById("btnDelete").addEventListener("click", function () {
      console.log("삭제 실행");
    });
  }
  // 실행
  setEvent();
</script>
```

---

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [바닐라 자바스크립트](http://www.yes24.com/Product/Goods/105608999)  
> [https://dinfree.com/lecture/frontend/123_js_3.html#m1](https://dinfree.com/lecture/frontend/123_js_3.html#m1)
