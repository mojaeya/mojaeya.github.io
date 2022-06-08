---
layout: post
title: 자바스크립트에서 DOM 조작하기
category: JavaScript
tags: [javascript, dom]
comments: true
---

## DOM(Document Object Model)

자바스크립트는 HTML 문서의 모든 요소에 접근하여 변경할 수 있다. 사용자가 웹 페이지에 접근하면 웹 페이지가 로드되면서 브라우저는 웹 페이지에 대한 `DOM(Document Object Model)`을 생성하게 된다.
`DOM`은 HTML 문서에 접근하기 위한 표준을 정의하며 일종의 인터페이스이다.

HTML DOM 모델은 `객체트리`로 구성된다.

<p align='center'><img width="514" alt="스크린샷 2022-05-14 오후 10 02 11" src="https://user-images.githubusercontent.com/76654131/168426888-b4b1c552-ff19-47f9-be66-9334cad0f141.png"></p>

---

사용자가 브라우저에 입력하는 데이터는 DOM 요소의 `value` 속성에 저장된다.  
결국 우리는 사용자 데이터를 자바스크립트에서 가져와서 사용하려면

1. 먼저 DOM 요소에 접근을 한 뒤
2. 해당 요소 속성 정보에 접근해야 한다.

## DOM 요소(element)에 접근하기

#### `예제 1`

<img width="228" alt="스크린샷 2022-05-15 오후 2 22 17" src="https://user-images.githubusercontent.com/76654131/168458404-d3c0c569-604f-4d11-855e-fc92839366e3.png">

```html
<!-- <body> -->
<div>
  <label for="userId">사용자 ID</label>
  <input type="text" name="" id="userId" class="form-control" />
</div>
<!-- <script> -->
```

### 1. id 값을 이용해서 DOM 요소 찾기

document 객체의 내장 함수인 `getElementByID` 를 사용하여 HTML 요소에 대한 접근이 가능하다.

```html
<script>
  const userIdElement = document.getElementById("userId");
  // console.log(userIdElement);
</script>
```

### 2. 태그명을 이용해서 DOM 요소 찾기

`getElementsByTagName` : 파라미터로 전달한 태그명에 해당하는 모든 HTML 요소 반환

```html
<script>
  const labelElements = document.getElementsByTagName("label");
  // console.log(labelElements);
</script>
```

### 3. 클래스명을 이용해서 DOM 요소 찾기

`getElementsByClassName` : 파라미터로 전달한 클래스명과 동일한 class 속성값을 포함하고 있는 모든 HTML 요소 반환

```html
<script>
  const inputElements = document.getElementsByClassName("form-control");
  // console.log(inputElements);
</script>
```

---

#### `예제 2`

<img width="226" alt="스크린샷 2022-05-15 오후 2 21 16" src="https://user-images.githubusercontent.com/76654131/168458384-ad2e6a88-7770-4965-b04e-82799849867b.png">

```html
<!-- <body> -->
<div>
  <input type="checkbox" name="chk_pl" id="chk_html" value="HTML" />
  <label for="chk_html">HTML</label>
  <input type="checkbox" name="chk_pl" id="chk_css" value="CSS" />
  <label for="chk_css">CSS</label>
  <input type="checkbox" name="chk_pl" id="chk_js" value="JS" />
  <label for="chk_js">JavaScript</label>
</div>
<button onclick="doSave();">저장</button>
<!-- <script> -->
```

### 4. name 속성 값을 이용해서 DOM 요소 찾기

`getElementsByName` : 파리미터로 전달한 name 값과 동일한 name 속성값을 포함하고 있는 모든 HTML 요소 반환

```html
<script>
  function doSave() {
    const chks = document.getElementsByName("chk_pl");
    // console.log(chks);
    // "chk_pl" 이라는 name 속성값을 포함하고 있는 모든 HTML 요소를 불러온 뒤,
    let checkedValue = [];
    for (const chk of chks) {
      if (chk.checked) {
        // checked 메소드를 사용해서 체크된 값들만 걸러준다.
        checkedValue.push(chk.value);
      }
    }
    // console.log(checkedValue);
  }
</script>
```

### <font color='red'>5. CSS 선택자를 이용해서 DOM 요소 찾기</font>

document 객체의 내장 함수인 `querySelector`, `querySelectorAll` 을 사용하면 파라미터로 CSS 선택자를 사용할 수 있다. getElementByXXX() 와 달리 단일 메서드로 원하는 요소를 찾을 수 있다.

- **`querySelector()`**

지정된 선택자와 일치하는 document의 첫 번째 element를 반환하고 종료된다. 일치하는 요소가 없으면 null을 반환한다. (한건) ex 유일한 값을 가진 id 선택자

- **`querySelectorAll()`**

지정된 셀렉터 그룹에 일치하는 document의 element list를 나타낸다. 즉 NodeList를 반환한다.
지정된 셀렉터가 없는 경우에는 비어있는 NodeList로 반환된다. (여러건)

```html
<script>
  function doSave() {
    const checkedElements = document.querySelectorAll("[name=chk_pl]:checked");
    // console.log(checkedElements);
    // css 가상 클래스 선택자 ":checked" 를 이용해서 "chk_pl" 이라는 name 속성값을 포함하고 있는
    // *체크된 HTML 요소만* 불러온다.
    let checkedValue = [];
    for (const chk of checkedElements) {
      checkedValue.push(chk.value);
    }
    // console.log(checkedValue);
  }
</script>
```

이렇게 CSS선택자를 이용해서 접근하면 HTML 태그나 속성값들을 이용해서 DOM에 접근하는 것보다  
**<font color='#1E90FF'>훨씬 간단하고 유용하다.</font>**

---

## DOM 속성(attribute) 조작하기

이제 DOM 요소에 접근을 하였으니 DOM 요소가 가지고 있는 속성 정보를 읽어오거나, 값을 변경하는 등 조작할 수 있다.

`예제`

```html
<!-- <body> -->
<label for="selLanguage">가장 좋아하는 프로그래밍 언어는?</label>
<select name="" id="selLanguage" value="">
  <option value="HTML">HTML</option>
  <option value="CSS">CSS</option>
  <option value="JS">JavaScript</option>
</select>
<button onclick="doSave();">저장</button>
<button onclick="setLang();">설정</button>
<!-- <script> -->
```

```html
<script>
  function doSave() {
    const favoriteLang = document.querySelector("#selLanguage").value;
    console.log(favoriteLang);
  }

  function setLang() {
    document.querySelector("#selLanguage").value = "JS";
  }
</script>
```

![May-15-2022 15-20-50](https://user-images.githubusercontent.com/76654131/168460022-f7e04c7b-55ed-4d9d-a899-ee01cae6fa61.gif)

이렇게 value 메소드를 이용해 속성정보에 접근해 속성명을 읽어오거나, 값을 넣어서 변경해서 세팅해줄 수 있다.

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [바닐라 자바스크립트](http://www.yes24.com/Product/Goods/105608999)  
> [https://www.w3schools.com/js/js_htmldom.asp](https://www.w3schools.com/js/js_htmldom.asp)
