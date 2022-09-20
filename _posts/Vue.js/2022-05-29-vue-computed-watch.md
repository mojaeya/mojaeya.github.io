---
layout: post
title: Vue.js | computed와 watch
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI 5

`computed`와 `watch`는 **<mark style='background-color: #dcffe4'>Vue 인스턴스</mark>** 내의 정의된 데이터 값에 변경이 일어나는지를 검사하고, 변경될 때마다 정의된 함수가 실행된다. 하지만 데이터 값의 변경을 감시한다는 측면은 비슷하지만 사용되는 용도에 차이점 있으니 알아보자.

---

먼저 `computed`를 살펴보기 앞서,

DB에 사용자 정보를 저장하고 있고, 사용자의 이름을 firstName, lastName으로 구분해서 저장하고 있다고 가정해보자.

만약 화면에 사용자 이름을 fullName으로 합쳐서 보여줘야 하는 경우에 아래와 같이 두가지 방법으로 구현이 가능하다.

```html
<!-- <template> -->
<div>
  <p>{{ '{{ firstName ' }}}}, {{ '{{ lastName ' }}}}</p>
  <p>{{ '{{ getFullName ' }}}}</p>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      firstName: "John",
      lastName: "Doe",
    };
  },
  methods: {
    getFullName() {
      return this.firstName + " " + this.lastName;
    },
  },
};
```

그런데 이런 방식으로 사용자 이름을 화면 여러 곳에서 보여줘야 한다고 가정하면, 연산 및 함수 호출을 사용자 이름을 화면에 보여줘야하는 수 만큼 해줘야 한다.

그럼 이제 computed를 사용한 코드를 봐보자.

---

## computed

`computed` 내에 함수를 정의해서 사용하는데 아래 코드에서 함수명인 fullName은 함수이자 동시에, **<mark style='background-color: #dcffe4'>Vue 인스턴스</mark>**의 데이터 키 값이다.

```html
<!-- <template> -->
<div>
  <p>{{ '{{ fullName ' }}}}</p>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      firstName: "John",
      lastName: "Doe",
      //fullName
    };
  },
  computed: {
    fullName() {
      return this.firstName + ", " + this.lastName;
    },
  },
};
```

이렇게 `computed` 내에 함수를 정의하면 fullName 함수가 실행되어 데이터 fullName과 lastName이 합한 값이 할당되는 것이다.

또한 화면 여러 곳에서 fullName을 사용해도 이에 대한 연산은 한번 밖에 일어나지 않는다.

그리고 firstName, lastName 데이터의 값이 하나라도 변경이 일어나면 fullName 함수가 자동으로 실행되고, fullName 값이 갱신된다. (양방향 데이터 바인딩, 반응형)

위에서 `methods` 내에 함수를 정의해서 fullName을 계산한는 경우 데이터 값의 변경이 일어났을 때 실시간으로 감지를 할 수 없다는 점과 비교하면 연산 및 반응형 측면에서 매우 효율적이고 편리하다.

---

## watch

computed 의 경우 기존에 정의된 데이터 값을 기반으로 새로운 데이터 값을 활용하기 위해 사용된다면, `watch`는 watch에 정의된 데이터 값 하나만을 감시하기 위한 용도로 사용된다.

또한, `watch`의 경우 computed와 다르게 실제 데이터 변경이 일어나기 전까지 실행되지 않는다.

```html
<!-- <template> -->
<div>
  <p>{{ '{{ fullName ' }}}}</p>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      firstName: "John",
      lastName: "Doe",
      fullName: "",
    };
  },
  watch: {
    fullName() {
      this.fullName = this.firstName + ", " + this.lastName;
    },
    lastName() {
      this.fullName = this.firstName + ", " + this.lastName;
    },
  },
};
```

❗️ 위 코드를 실행하면 화면에 아무것도 출력되지 않는다  
firstName과 lastName의 초기 할당된 값이 변경이 일어나지 않았기 때문이다.

만약 fistName과 lastName의 값이 하나라도 변경이 된다면 `watch`가 감지하고 함수가 실행되면서
fullName이 갱신된다.

---

그리고 아래처럼 `watch` 내 함수에 두개의 인자를 주면 firstName이 변경되기전의 값과 변경된 후의 값이 넘어온다. (첫번째 인자로 새로운 값 그리고 두번째 인자로 이전값이 넘어온다)

```javascript
  watch: {
   firstName(newValue, oldValue) {
      console.log('oldValue', oldValue)
      console.log('newValue', newValue)
    },
  },
```

이러한 `watch`의 특성을 이용하면 사용자의 행동 패턴 등의 히스토리를 파악할 수 있어 서비스에 도움이 되는 데이터 수집이 가능하다.

```html
<!-- <template> -->
<div>
  <select name="" id="" v-model="selected">
    <option value="A">A</option>
    <option value="B">B</option>
    <option value="C">C</option>
  </select>
</div>
```

```javascript
// <script>
export default {
  data() {
    return {
      selected: "",
      changeHistory: [],
    };
  },
  watch: {
    selected(newValue, oldValue) {
      this.changeHistory.push(newValue);
    },
  },
};
```

---

## computed와 watch의 차이점

### ✔️ computed

정의된 데이터 값을 바탕으로 새로운 데이터 값을 생성하고, 새로운 데이터 값에서 참조하고 있는 기존 데이터 값의 변경을 감지한다.

그리고 참조하고 있는 데이터 값의 변경과 상관없이 최초의 `computed`에 정의된 데이터 함수를 실행한다.

### ✔️ watch

초기에 할당된 값에서 변경이 일어나야만 `watch`에 정의한 함수를 실행한다.

  <br>
  <br>
  <br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
