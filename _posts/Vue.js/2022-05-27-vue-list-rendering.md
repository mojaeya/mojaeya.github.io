---
layout: post
title: Vue.js | 리스트 렌더링(v-for)
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI

## 리스트 랜더링 List Rendering (v-for)

다중 데이터를 처리해야 할 때 리스트 랜더링 `v-for` 디렉티브를 이용한다.

제품 리스트처럼 동일한 UI 패턴에 데이터만 다르게 처리되는 부분들이 다중 데이터를 이용해서 처리되는 부분이라고 생각하면 된다.

select의 option, table의 tr 태그 등 반복적으로 랜더링 할 HTML 태그에 `v-for` 디렉티브를 사용하면 배열에 있는 데이터 수만큼 html 태그를 반복적으로 렌더링 한다.

#### v-for 디렉티브 사용 방법

```javascript
v-for = "(item, index) in items"
// items = 데이터 배열, item = 배열의 각 item, index = 배열의 현재 index
```

---

## 활용

### select의 option 태그

for in 반복문 쓰는 것처럼 `v-for` 디렉티브를 써주는데, 반드시 데이터의 <font color='red'>유일한 값</font>을 `key`로 잡아줘야 한다.

```html
<!-- <template> -->
<div>
  <select name="" id="">
    <option :value="city.code" :key="city.code" v-for="city in cities">
      {{ '{{ city.title ' }}}}
    </option>
  </select>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      cities: [
        { title: "서울", code: "02" },
        { title: "부산", code: "051" },
        { title: "제주", code: "064" },
      ],
    };
  },
};
```

---

### table의 tr 태그

```html
<!-- <template> -->
<div>
  <table>
    <thead>
      <tr>
        <th>제품번호</th>
        <th>제품명</th>
        <th>가격</th>
        <th>주문수량</th>
        <th>합계</th>
      </tr>
    </thead>
    <tbody>
      <tr :key="drink.drinkId" v-for="drink in drinkList">
        <td>{{ '{{ drink.drinkId ' }}}}</td>
        <td>{{ '{{ drink.drinkName ' }}}}</td>
        <td>{{ '{{ drink.price ' }}}}</td>
        <td><input type="text" name="" id="" v-model="drink.qty" /></td>
        <td>{{ '{{ drink.price * drink.qty ' }}}}</td>
      </tr>
    </tbody>
  </table>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      drinkList: [
        {
          drinkId: "1",
          drinkName: "코카콜라",
          price: 700,
          qty: 1,
        },
        {
          drinkId: "2",
          drinkName: "환타",
          price: 700,
          qty: 1,
        },
        {
          drinkId: "3",
          drinkName: "사이다",
          price: 700,
          qty: 1,
        },
      ],
    };
  },
};
```

#### 리스트 렌더링 적용 화면

<img width="378" alt="스크린샷 2022-06-20 오전 4 39 46" src="https://user-images.githubusercontent.com/76654131/174497645-559d2dfd-c2d4-4ff1-8b78-c8034dc42ff3.png">

---

✔️ **<mark style='background-color: #dcffe4'>Vue</mark>** 는 이렇게 `데이터바인딩`과 `v-for` 디렉티브 등의 특성을 이용해 바닐라 자바스크립트로 구현하는 것보다 훨씬 편리하고 빠르게 구현할 수 있다.

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
