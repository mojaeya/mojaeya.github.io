---
layout: post
title: Vue.js | Provide / Inject
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI

부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 경우 `props`를 사용하면 된다.

<p align='center'><img width="661" alt="스크린샷 2022-07-27 오후 3 55 09" src="https://user-images.githubusercontent.com/76654131/181181721-bf74658d-0556-40ff-9728-0e3eb80e4696.png"></p>

하지만 컴포넌트 계층 구조가 복잡해지고 자식의 자식 컴포넌트로 데이터를 전달해줘야 한다면❓  
`props`를 계속해서 쓰다가는 코드 구조가 굉장히 복잡해질 것이다.

이런 경우에 **<mark style='background-color: #dcffe4'>Vue</mark>**에서 제공하는 `Provide/Inject`를 사용하면 된다.

---

## Provide / Inject 적용 해보기

<p align='center'><img width="635" alt="스크린샷 2022-07-27 오후 3 55 16" src="https://user-images.githubusercontent.com/76654131/181181712-011d75f3-b608-4532-9e25-72d1b48043d8.png">
</p>

위 그림처럼 자식의 자식 컴포넌트까지 구성한 다음 `Provide / Inject`를 사용하는 것이 아니고,  
편의상 자식 컴포넌트 하나만을 가지고 이것을 어떤 컴포넌트가 쓰고 있다고 가정하고 기능을 적용시켜보겠다.

### ✔️ 부모 컴포넌트에서 자식 컴포넌트로 전달하고자 하는 데이터를 `provide`에 정의한다.

#### > src / views / ProvideView.vue

```html
<template>
  <div>
    <provide-inject />
  </div>
</template>
```

```javascript
// <script>
import ProvideInject from "@/components/ProvideInject.vue";
export default {
  components: { ProvideInject },
  provide() {
    return {
      size: 5,
      str: this.sampleData,
    };
  },
  data() {
    return {
      sampleData: "AAA",
    };
  },
};
```

---

### ✔️ 부모 컴포넌트로부터 전달받고자 하는 데이터와 동일한 속성 이름으로 `inject`에 문자열 배열로 정의한다.

#### > src / components / ProvideInject.vue

```html
<template>
  <div>
    <p>{{ '{{ size ' }}}}</p>
    <p>{{ '{{ str ' }}}}</p>
  </div>
</template>
```

```javascript
// <script>
export default {
  inject: ["size", "str"],
};
```

---

이렇게 `Provide / Inject`를 이용하면 컴포넌트 계층 구조가 복잡하더라도 `props` 없이 `편리하게` 자식 컴포넌트로 데이터를 한번에 전달할 수 있다.

❗️ 하지만 이렇게 `inject`를 통해서 전달받는 자식 컴포넌트에서는 `props`를 쓸 때와 달리 어떤 부모 컴포넌트에서 이 데이터가 전달되는지 명확히 확인이 안된다는 단점이 있다. 그러므로 편리함만을 생각해서 무작정 쓰지 말고 필요할 상황에 적절하게 쓰는 것을 권장한다.

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)  
> [https://vuejs.org/guide/components/provide-inject.html#working-with-reactivity](https://vuejs.org/guide/components/provide-inject.html#working-with-reactivity)
