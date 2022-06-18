---
layout: post
title: DOM Events (load, unload, change, focus, blur, scroll, preventDefault())
category: JavaScript
tags: [javascript, dom]
comments: true
---

<br>

[이전 포스팅](https://mojaeya.github.io/javascript/2022/05/15/domEvent-Handler/)에서 DOM 이벤트와 이벤트 핸들러 개념을 click 이벤트를 예시로 들어 알아보았는데,  
이번 포스팅에서는 click 이벤트 외의 대표적인 DOM 이벤트들을 알아보자.

---

## HTML DOM Events

### > `load` 이벤트

- HTML 태그가 DOM 객체 트리 모델로 모두 추가가 되었을 때 발생

사용자가 웹 페이지에 접근하는 순간 자바스크립트 엔진이 HTML DOM 객체 트리를 구성하는데,  
HTML 구조가 복잡하고 방대할 경우 HTML DOM 객체 트리를 다 만들기도 전에 <font color='#1E90FF'>script가 먼저 실행되는 경우</font>가 발생할 수 있다. 이러한 경우 script 안에 작성해둔 이벤트 함수들이 HTML 코드를 못 찾아 <font color='red'>에러가 발생한다.</font>

이럴 때 `load` 이벤트를 사용하면 `에러 없이 안전하게 사용할 수 있다.`

```html
<body>
  <button id="btnSave">저장</button>
  <!-- 수많은 html 태그 ...  -->
  . . .
</body>

<script>
  function setEvent() {
    document.querySelector("#btnSave").addEventListener("click", function () {
      console.log("저장 실행");
    });
    //  수많은 이벤트 함수...
  }

  // load 이벤트 - HTML 태그가 DOM 객체 트리 모델로 모두 추가가 되었을 때만 발생
  window.addEventListener("load", function () {
    setEvent();
  });
</script>
```

---

### > `unload` 이벤트

- 현재 페이지에서 다른 페이지로 이동할때, 혹은 페이지를 닫을 때 발생
- ex) 메모리 관리, 기업 시스템 보안 측면에서 창 닫을 때 로그아웃 시켜주는 기능

```html
<script>
  window.addEventListener("unload", function () {
    // arrBigData = null; -> 메모리 효율적 관리
  });
</script>
```

---

### > `change` 이벤트

- 요소값 변경이 끝나면 발생
- select 와 input type=checkbox, radio는 선택 값이 변경된 직후에 이벤트가 발생
- input type=text : 텍스트 입력 요소인 경우에는 버튼 클릭 등으로 포커스를 잃을 때 이벤트가 발생

```html
<body>
  <select name="" id="sel">
    <option value="KO">Korea</option>
    <option value="CN">China</option>
    <option value="JP">Japan</option>
  </select>
</body>

<script>
  document.querySelector("#sel").addEventListener("change", function () {
    console.log(document.querySelector("#sel").value); // 선택된 value 출력
  });
</script>
```

---

### > `focus`, `blur` 이벤트

- `focus` 이벤트는 요소가 포커스를 받을 때, `blur` 이벤트는 포커스를 잃을 때 발생

`blur 이벤트 예시`

```html
<body>
  <input type="text" name="" id="str" />
  <span id="strMsg" style="display: none; color: red">필수 입력 값입니다.</span>
</body>

<script>
  // blur - 포커스가 빠져나올때
  document.querySelector("#str").addEventListener("blur", function () {
    // 입력 값이 없으면
    if (document.querySelector("#str").value === "") {
      document.querySelector("#strMsg").style.display = ""; // 필수 입력 값입니다 -> 화면에 출력 후
      document.querySelector("#str").focus(); // 입력창으로 자동 포커스 (focus 이벤트와 무관한 메소드임)
    } else {
      document.querySelector("#strMsg").style.display = "none";
    }
  });
</script>
```

![Jun-08-2022
17-07-27](https://user-images.githubusercontent.com/76654131/172565495-62a43dbc-b966-42b0-8a9c-271fc81a228b.gif)

---

### > `scroll` 이벤트

- document view나 element가 스크롤 될 때 발생

스크롤 이벤트는 스크롤이 움직일 때마다 작동하기 때문에 매우 빠른 속도로 실행된다.  
그래서 콘솔에 window.scrollY 를 찍어보면 엄청나게 많은 스크롤 값들을 확인할 수 있다.

> Window 인터페이스의 scrollY - 문서가 수직으로 얼마나 스크롤됐는지 픽셀 단위로 반환  
> 수평 스크롤은 scrollX

![Jun-08-2022 22-48-33](https://user-images.githubusercontent.com/76654131/172633110-86217706-f164-44a8-90f7-14f6fbdace32.gif)

이러한 `scrollY` 위치 값을 `scroll` 이벤트 함수 안에서 사용하면,

흔히 웹사이트에서 `글을 한참 내리다가 오른쪽 하단에 생기는 버튼`을 누르면 위로 스르륵 올라가는 (scrollTop = 0) 기능을 구현할 수 있다.

스크롤에 위치에 따라 올라가는 버튼이 생기고 안생기는 부분은 잘못하면,

`DOM 트리`에 <font color='red'>접근을 과도하게 많이해서 자원을 소비하는 문제</font>가 발생할 수 있기 때문에 코드 상에 showScrollBtn = true / false 같이 제어장치를 만들어 보이지 않는 과도한 자원 소비를 줄이는게 중요하다.

```html
<body onscroll="checkScroll();">
  <button id="btnTop" style="">누르면 올라가는 버튼</button>
</body>

<script>
  let showScrollBtn = false;

  function checkScroll() {
    if (window.scrollY > 400 && !showScrollBtn) {
      showScrollBtn = true;
      document.querySelector("#btnTop").style.display = "";
    } else if (window.scrollY <= 400 && showScrollBtn) {
      showScrollBtn = false;
      document.querySelector("#btnTop").style.display = "none";
    }
  }

  window.addEventListener("load", function () {
    document.querySelector("#btnTop").addEventListener("click", function () {
      document.documentElement.scrollTop = 0;
    });
  });
</script>
```

---

### > `preventDefault()` 이벤트 메서드

- 이벤트의 기본 동작을 중지

```html
<script>
  // contextmenu - 마우스 오른쪽 클릭하면 메뉴 선택 이벤트
  document.addEventListener("contextmenu", function () {
    event.preventDefault(); // 화면상에서 마우스 우클릭해도 메뉴 선택창 안뜸
  });
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
