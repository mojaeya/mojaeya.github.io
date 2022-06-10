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

(함수의 인자로 event 객체가 전달된다. 함수 정의시 인자로 선언 안해도 자동 전달된다. 그래서 event.target 등으로 이벤트가 발생한 대상(요소)를 얻어올 수 있는 것이다.)

---

## 이벤트 처리 방법 3가지

`예시 : click 이벤트`

#### 1. HTML 태그의 속성으로 정의하는 형식

- HTML 문서를 읽어들일 때 이벤트 처리기도 함께 설정하기 때문에 설정하기 쉽다.

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

- HTML과 자바스크립트를 분리해서 작성 가능하기 때문에 프로그램 유지 보수성 향상

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

#### 3. <font color='red'>addEventHandler()</font>를 이용한 이벤트 핸들러를 추가하는 형식 `- DOM Level 2부터 추가`

- 이벤트 요소를 추가하기 위한 가장 구조적인 방법으로 onclick 속성에 콜백 함수를 구현하는 것 보다 좋은 방법.

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

> addEventListener로 등록한 함수는 이벤트 리스너, 그 외 방법으로 등록한 함수는 이벤트 핸들러(처리기)
> 라고 부른다.

#### `기존 이벤트 핸들러`

- HTML 태그의 속성으로 정의하는 형식
- 자바스크립트에서 DOM 엘리먼트의 속성에 콜백 함수를 정의하는 형식

#### `DOM Level 2부터 추가된 이벤트 리스너`

- addEventHandler()를 이용한 이벤트 핸들러를 추가하는 형식

---

## 기존 이벤트 핸들러의 문제점

### 1. HTML 태그의 속성으로 정의하는 형식의 문제 <br> `- 프로그램 유지 보수성 떨어짐` 😂

`HTML 태그에 직접 이벤트가 달려있으면` 예를 들어 나중에 퍼블리셔나 웹디자이너분들이 화면 변경을 하거나, 구조를 바꾸는 경우 다시 일일이 새로 받은 HTML에 이벤트를 다시 걸어줘야하는 <font color='red'>번거로운</font> 경우가 발생한다.

#### > 반면, `DOM 프로퍼티, addEventHandler()`를 이용한 이벤트 처리 형식 `- 프로그램 유지 보수성 향상` 😊

`자바스크립트 안에서 따로 이벤트 관리`를 하고 있다면, 화면이 많이 변경이 된다고 해도 새로운 HTML 태그에 이벤트를 달아주는 <font color='#1E90FF'>불필요한 작업이 필요없게 된다.</font>

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

### 2. HTML 속성과 DOM 프로퍼티를 이용한 이벤트 핸들러 형식의 근본적인 문제 <br> `- 하나의 이벤트에 복수의 핸들러를 할당할 수 없다.`

특정 요소의 특정 이벤트에 단 하나의 이벤트 처리기만 등록 가능하다.  
같은 요소에 똑같은 이벤트를 처리하는 이벤트 처리기를 등록하면 나중에 등록한 함수가 이전 함수를 덮어쓰게 되는 문제가 생긴다.

```html
<body>
  input.onclick = function() { alert(1); }
  <!-- ... -->
  input.onclick = function() { alert(2); } // 이전 핸들러를 덮어씀
</body>
```

### <font color='#1E90FF'>해결</font>

- `addEventHandler()`를 이용한 이벤트 핸들러 추가

개발자들은 오래전부터 이러한 문제를 인지하고, `addEventListener` 와 `removeEventListener` 라는 특별한 메서드를 이용해 핸들러를 관리하자는 대안을 제시했다. `핸들러를 여러 개 할당할 수 있도록 말이다.`

```html
<input id="elem" type="button" value="클릭해 주세요." />

<script>
  function handler1() {
    alert("감사합니다!");
  }

  function handler2() {
    alert("다시 한번 감사합니다!");
  }

  elem.onclick = () => alert("안녕하세요.");
  elem.addEventListener("click", handler1); // 감사합니다!
  elem.addEventListener("click", handler2); // 다시 한번 감사합니다!
</script>
```

---

## 결론

프로그램 유지 관리 보수성, 가독성, 핸들러 복수 추가 등 여러가지 측면에서 가장 나은,  
`addEventHandler()`를 이용한 이벤트 핸들러를 추가하는 형식을 사용하는것을 추천한다.

---

> 여담

#### 위에서 해결 예시 코드를 보면 document.getElementById('id') 같은 메소드를 안써도 작동이 되네?

id와 동일한 이름의 전역변수가 만들어지기 때문에 id.addEventListener(...) 사용이 가능하다.

그런데, 이 기능은 과거 코드와의 하위 호환성을 위해서 남겨진 것이므로,
`getElementById()` , `querySelector()` 함수를 써서 직접 해당 태그에 대한
변수를 생성한 다음 사용하는 것이 안전하다고 한다.

만약 코드가 복잡해져서 id와 동일한 로컬 변수(let id)가 만들어지면 앞에서 말한 그 태그는 더 이상 id.xxx 등으로 접근할 수 없게 되기 때문이다. 참고!

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [바닐라 자바스크립트](http://www.yes24.com/Product/Goods/105608999)  
> [https://dinfree.com/lecture/frontend/123_js_3.html#m1](https://dinfree.com/lecture/frontend/123_js_3.html#m1)  
> [https://pathas.tistory.com/213](https://pathas.tistory.com/213)  
> [https://ko.javascript.info/introduction-browser-events#ref-624](https://ko.javascript.info/introduction-browser-events#ref-624)
