---
layout: post
title: DOM Events (Bubbling, Capturing )
category: JavaScript
tags: [javascript, dom]
comments: true
---

## 이벤트 버블링(Bubbling)

- 이벤트가 발생한 노드에서 최상위 노으로 이벤트가 순차적으로 전파되는 것을 **`이벤트 버블링`**이라고 한다.

<p align='center'><img width="352" alt="스크린샷 2022-06-10 오후 10 40 01" src="https://user-images.githubusercontent.com/76654131/173078231-2fba3b5e-9951-4a63-96ca-1e60698aed1d.png">
</p>

```html
<!-- <style> -->

<body>
  <div class="parent-parent" onclick="parentParentFunction();">
    DIV 이벤트 실행
    <div class="parent">
      div 이벤트 실행 및 버블링
      <p class="child" onclick="childFunction();">p 이벤트 실행 및 버블링</p>
    </div>
  </div>
</body>

<script>
  function childFunction() {
    console.log(event.path);
  }

  function parentParentFunction() {
    console.log("parentParentFunction");
  }
</script>
```

<img width="495" alt="스크린샷 2022-06-10 오후 10 43 04" src="https://user-images.githubusercontent.com/76654131/173078819-d04f10ba-53d6-45cd-9077-2905d7d92acc.png">

위 그림은 가장 안쪽의 빨간색 박스칸을 클릭했을 때 이벤트가 최상위 노드로 순차적으로 발생하는 모습을 콘솔에 보여주고 있다.

`event.path` 를 찍어보면 이벤트가 버블링 되고 있는 구조를 순차적으로 알 수 있다.

결국 마지막 최상위 노드인 parent-parent 클래스 요소까지 가서 `click` 이벤트가 발생함을 볼 수 있다.

이것이 **`이벤트 버블링(bubbling)`**이다.

---

### > `stopPropagation()` 이벤트 메서드

그런데 저렇게 이벤트를 따로 따로 줬다는 것은 <font color='#1E90FF'>개별로</font> 동작하게 끔 하고 싶어서 그런건데,  
`이벤트 버블링`에 의해서 <font color='red'>한동작에 의해 모든 이벤트가 발생</font>하면 안되지 않겠나?

그래서 이러한 이벤트 버블링을 막기 위해서는 **`stopPropagation()`** 이벤트 메서드를 사용해야 한다.

```html
<!-- <style> -->

<!-- <body> -->

<script>
  function childFunction() {
    event.stopPropagation(); // 이벤트 버블링 중지
  }
  //...
</script>
```

---

> 참고

#### ❗️ 꼭 필요한 경우를 제외하곤 버블링을 막지 마라!

이벤트 버블링은 유용하지만 실제로 이벤트 버블링을 막아야 하는 경우는 없다고 한다.  
이벤트 버블링을 막아야 해결되는 문제라면 보통 커스텀 이벤트 등을 사용해 해결한다.

그러므로 버블링을 꼭 멈춰야하는 상황이 아니면 함부로 막지 말고 아키텍처를 잘 고려하며 써야 한다!

---

## 이벤트 캡처링(capturing)

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [바닐라 자바스크립트](http://www.yes24.com/Product/Goods/105608999)  
> [https://ko.javascript.info/bubbling-and-capturing](https://ko.javascript.info/bubbling-and-capturing)
