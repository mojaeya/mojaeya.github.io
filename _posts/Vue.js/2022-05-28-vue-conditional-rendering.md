---
layout: post
title: Vue.js | 조건부 렌더링(v-if, v-show)
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI 5

## 조건부 렌더링 Conditional Rendering

바닐라 자바스크립트에서 style.display 속성을 이용해서 HTML DOM을 화면상에서 보였다 안보였다 하는 방법을  
**<mark style='background-color: #dcffe4'>Vue</mark>**에서는 `v-if`, `v-show` 디렉티브를 사용한다.

---

## v-if

if문처럼 elseif else 표현식이 사용 가능하다.

`v-if` 디렉티브에 <font color='#1E90FF'>true</font>가 리턴되면 HTML 블록이 렌더링 되고, <font color='red'>false</font>인 경우 화면에 렌더링이 안된다.

```html
<!-- <template> -->
<div v-if="userRole === 'G'">
  <button>조회</button>
</div>
<div v-else-if="userRole === 'M'">
  <button>조회</button>
  <button>생성</button>
</div>
<div v-else>
  <button>조회</button>
  <button>생성</button>
  <button>삭제</button>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      userRole: "M", // A(Admin) - 관리자, M(Manager) - 매니저, G(General) - 일반사용자
    };
  },
};
```

별거 아니지만 어떠한 시스템을 사용하는 대다수의 이용자의 특성을 고려해서  
위 코드처럼 일반사용자 조건을 맨 앞 코드에 두는 사소한 습관? 생각을 가지는게 중요하다.

---

## v-show

`v-show`의 경우도 조건 성립 여부에 따라 화면에 렌더링된다.

```html
<h1 v-show="bShow">bShow가 true면, 현재 블록이 화면에 렌더링</h1>
```

---

## v-if 와 v-show의 차이점

`v-if`와 `v-show`는 비슷해 보이지만, 내부적으로 렌더링 되는 방식에 큰 차이가 있다.

`v-if`의 경우 조건을 만족하는 <font color='#1E90FF'>true</font>면 그 순간에 html 블록이 생성되고, <font color='red'>false</font>인 경우 html 블록이 삭제가 된다.

![Jun-20-2022 06-31-58](https://user-images.githubusercontent.com/76654131/174501121-b9ec3c4b-fc7e-42fa-8f29-c1877aa4582e.gif)

`v-show`의 경우 조건 만족 여부에 상관없이 무조건 html 블록이 생성된다.  
조건을 만족하는 <font color='#1E90FF'>true</font>면 CSS display를 이용해서 화면에 렌더링되게 하고 <font color='red'>false</font>인 경우 화면에서 숨기는 것이다.  
<u>즉, 무조건 렌더링이 되고 보는 것이다.</u>

![Jun-20-2022 06-31-51](https://user-images.githubusercontent.com/76654131/174501117-2a6fdfbb-f39a-4319-9d50-4510923158e3.gif)

---

## 그럼 언제 무엇을 쓰는게 좋을까?

`v-if`는 실제로 해당 블록 전체를 생성했다가 삭제하기 때문에 v-show보다 더 많은 자원을 소비한다.

`v-show`는 초기에 무조건 html 블록을 생성하는데 자원을 소비한다.

#### 그렇기에 해당 html 블록이 화면 내에서 자주 toggle이 일어나면 `v-show`, <br> 빈도가 작다면 `v-if`를 사용하는것이 좋다.

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
