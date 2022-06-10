---
layout: post
title: DOM Events (Keyboard, input)
category: JavaScript
tags: [javascript, dom]
comments: true
---

## Keyboard 이벤트

### > Keyboard : `keydown`, ~~`keypress`~~, `keyup` 이벤트

> 현재 keypress 이벤트 타입은 deprecated 되어 권장되지 않는다.
> <img width="517" alt="스크린샷 2022-06-10 오후 6 07 34" src="https://user-images.githubusercontent.com/76654131/173032051-c227f1da-9cf8-4ff7-8986-b4bf245f8c8e.png">

#### keydown -> ~~keypress~~ -> keyup 순으로 이벤트 진행

- `keydown` - 키를 누르는 동작 자체에 반응한다.
- ~~`keypress`~~ - 키를 누르고 있을 때 실행된다.
- `keyup` - 누른 키에서 손을 뗄 때 실행된다. 이 때 화면에 출력되어 사용자 눈에 보이게 된다.

❗️ `keyup` 이벤트 시점에 <u>사용자가 입력한 값이</u> <font color='red'>value 속성에 들어간다.</font>

![Jun-10-2022 17-49-54](https://user-images.githubusercontent.com/76654131/173028836-bae5e84c-300d-41b0-bb7d-5dd11d315c63.gif)

---

## 활용

> **이벤트 핸들러** : 함수의 인자로 **event 객체**가 전달된다. 함수 정의시 인자로 선언 안해도 자동 전달된다. 그래서 **event.target** 등으로 이벤트가 발생한 대상(요소)를 얻어올 수 있는 것이다.

### > `keyup` 이벤트 - 예시) 주민번호 입력 화면

사용자가 주민번호 앞자리 6자리를 입력하면 자동으로 다음칸으로 넘어가게 하는 편리함을 제공하는 것이 개발자의 의무이다.

![Jun-10-2022 18-16-01](https://user-images.githubusercontent.com/76654131/173033590-8f7544c2-a903-4b21-a133-ed394472afee.gif)

```html
<body>
  <input type="text" name="" id="id1" onkeyup="moveNext();" />-<input
    type="text"
    name=""
    id="id2"
  />
</body>

<script>
  function moveNext() {
    if (event.target.value.length === 6) {
      document.querySelector("#id2").focus();
    }
  }
</script>
```

### > ~~`keypress`~~ 이벤트 - 예시) 숫자만 입력되게!

```html
<body>
  <input type="text" name="" id="" onkeypress="onlyNumber();" />
</body>

<script>
  function onlyNumber() {
    // 숫자 0의 keyCode : 48
    // 숫자 9의 keyCode : 57
    if (event.keyCode >= 48 && event.keyCode <= 57) {
    } else {
      event.preventDefault(); // 이벤트 중지 시킴 -> keyup 이벤트로 안넘어가서 화면상에 출력 X
    }
  }
</script>
```

예전에는 이렇게 ~~`keypress`~~ 이벤트와 숫자 `keyCode` 를 가지고 숫자만 입력되게 막았었는데,

<font color='red'>한글 입력을 못막는</font>치명적인 단점이 있었다.

그래서 추가된 것이 `input` 이벤트이다.

---

## `input` 이벤트

#### keydown -> ~~keypress~~ -> input -> keyup 순으로 진행

- `keyup` 이벤트 일어나는 순간에 value 속성 값에 값이 들어감. 화면에 출력되어 사용자 눈에 보이게 됨.
- `input` 이벤트 일어나는 순간에 value 속성 값에 값이 들어감. 화면 출력 X 사용자 눈에는 안 보임.

이러한 원리를 이용해서 `input` 이벤트로 코드를 짜면 <font color='red'>아까 위에서 봤던 단점</font>을 해결할 수 있다.

```html
<body>
  <label for="number">숫자만 입력 가능한 필드</label>
  <input type="text" name="" id="number" oninput="onlyNumber();" />
</body>

<script>
  function onlyNumber() {
    const regexp = /\D/g; // 숫자가 아닌 모든 문자를 모두 찾아라
    event.target.value = event.target.value.replace(regexp, "");
  }
</script>
```

---

## 참고

#### ❗️ KeyboardEvent.`keyCode`도 <font color='red'>deprecated</font> 되어 권장되지 않음.

대안으로 **`key property`** 사용 권장!

다만, 아직은 `key property`를 지원하지 않는 브라우저가 있을 수 있으니 `아래 코드`처럼 이중으로 적용하는게 안전하다.

```html
<body>
  <textarea id="my-textarea"></textarea>
</body>

<script>
  function submitTextarea(event) {
    let key = event.key || event.keyCode; // key property - undefined 일 경우 keyCode로 동작

    if (key === "Enter" || key === 13) {
      alert("전송");
    }
  }

  let textarea = document.getElementById("my-textarea");
  textarea.addEventListener("keyup", (event) => submitTextarea(event));
</script>
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [바닐라 자바스크립트](http://www.yes24.com/Product/Goods/105608999)  
> [https://way-be-developer.tistory.com/244](https://way-be-developer.tistory.com/244)
