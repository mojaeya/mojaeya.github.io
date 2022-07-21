---
layout: post
title: Vue.js | 재사용 컴포넌트 심화
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI

[이전 포스팅](https://mojaeya.github.io/vue.js/2022/06/03/vue-reuse-component-basic/)을 읽고 오시면 도움이 됩니다.

---

## 자식 컴포넌트에서 부모 컴포넌트로 이벤트/데이터 전달하기 (커스텀 이벤트)

자식 컴포넌트에서 부모 컴포넌트로 이벤트를 전달할 때는 `$emit`을 사용한다.

자식 컴포넌트가 `mounted` 되면 `$emit`을 통해 부모 컴포넌트에 만들어둔 커스텀 이벤트 `send-msg` 이벤트를 호출한다.  
그리고 `두번째 파라미터`로 `데이터를 전송`한다.

#### > components / ChildComponent.vue (자식 컴포넌트)

```javascript
// <script>
export default {
  data() {
    return {
      msg: "자식 컴포넌트로부터 부모 컴포넌트로 메시지 전달",
    };
  },
  mounted() {
    this.$emit("send-msg", this.msg); // 부모 컴포넌트의 커스텀 이벤트 `send-msg` 호출
  },
};
```

그리고 부모 컴포넌트에서 자식 컴포넌트인 `ChildComponent` 를 `import` 하고 있으면,  
부모 컴포넌트에 정의된 `sendMsg` 함수가 실행된다.

그래서 자식 컴포넌트로부터 전달받은 데이터를 부모 컴포넌트에서 사용할 수 있는 것이다.

#### > views / ParentView.vue (부모 컴포넌트)

```html
<!-- <template> -->
<div>
  <child-component @send-msg="sendMsg" />
</div>
```

```javascript
// <script>
import ChildComponent from '@/components/ChildComponent.vue'
export default {
  components: { ChildComponent },
  methods: {
    sendMsg(data) { // `data` 파라미터에는 자식 컴포넌트에서 두번째 파라미터로 보낸 그 값이 들어간다.
        console.log(data)
    }
  }
```

---

## 부모 컴포넌트에서 자식 컴포넌트의 데이터 값 직접 변경하기

자식 컴포넌트에는 데이터 옵션에 `msg` 가 정의되어있다.

#### > components / ChildComponent.vue (자식 컴포넌트)

```html
<template>
  <h1>{{ '{{ msg ' }}}}}</h1>
</template>
```

```javascript
// <script>
export default {
  data() {
    return {
      msg: "",
    };
  },
};
```

`ref`는 쉽게 생각하면 **<mark style='background-color: #dcffe4'>Vue</mark>**에서 쓰는 `html`에서의 `id`라고 생각하면 쉽다.

유일한 값이 들어가야 하며, 우리가 `html`에서 `document.getElementByID()`를 사용하여 HTML 요소에 대한 접근한 것 처럼 `ref 값`으로 자식컴포넌트에 접근할 수 있게 된다.

(**<mark style='background-color: #dcffe4'>Vue</mark>**에서는 id 보다는 `ref` 가지고 접근을 많이 한다.)

접근하는 방법은 `$refs`를 이용하는 것이고,  
접근하고 나면 자식 컴포넌트에 정의된 데이터(예제에서는 'msg')를 직접 변경할 수 있게 된다.

#### > views / ParentView.vue (부모 컴포넌트)

```html
<!-- <template> -->
<div>
  <child-component @send-msg="sendMsg" ref="child_component" />
  <button @click="changeChildData">데이터 변경</button>
</div>
```

```javascript
// <script>
import ChildComponent from '@/components/ChildComponent.vue'
export default {
  components: { ChildComponent },
  methods: {
   changeChildData() {
    this.$refs.child_component.msg = "부모 컴포넌트가 변경한 데이터"
   }
  }
```

---

✔️ 만약 자식컴포넌트에 함수가 정의되어 있다면 똑같은 방법으로 부모 컴포넌트에서 자식 컴포넌트의 함수를 직접 호출할 수도있다.

✔️ 또한 부모 컴포넌트에서 computed를 이용하면, 자식 컴포넌트에 정의된 데이터 값의 변경사항을 항상 동기화시킬 수도 있다.
(computed를 이용하면 자식 컴포넌트의 데이터가 변경될 때마다 $emit을 통해 변경된 데이터를 전송하지 않아도 된다.)

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
