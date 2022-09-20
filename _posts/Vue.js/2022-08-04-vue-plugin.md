---
layout: post
title: Vue.js | Plugins
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI 5

`Plugin(플러그인)`은 특정 기능을 제공하는 코드이다. 그런데 우리는 이미 플러그인들을 설치해서 사용하고 있다.  
`npm`으로 설치했던 패키지들도 `플러그인` 이기 때문이다. 플러그인은 모듈로, 때로는 패키지로 사용될 수 있다.

**<mark style='background-color: #dcffe4'>Vue</mark>** 에서도 여러 컴포넌트에서 사용할 수 있는 공통기능에 해당하는 함수를 마치 `플러그인을 설치`하는 것처럼 사용할 수 있게끔 제공한다 해서 `Plugin` 이라고 얘기하고 있다.

이번 포스팅에서는 `다국어(i18n)를 처리해주는 플러그인`을 제작해보자.

---

## 다국어(i18n) 처리 플러그인 생성

플러그인은 `install` 옵션에서 정의해서 사용할 수 있다.

- `app.config.globalProperties` - App 내의 모든 컴포넌트 인스턴스에서 접근할 수 있는 전역 속성을 추가  
  (전역변수 설정)

아래 예제의 경우 컴포넌트에서 `$tranlate` 로 바로 접근해서 사용 가능

#### > src / plugins / i18n.js

```javascript
export default {
  install: (app, options) => {
    app.config.globalProperties.$translate = (key) => {
      // key.split(".") : en.hi => ['en','hi']
      return key.split(".").reduce((o, i) => {
        if (o) return o[i];
      }, options);
    };
  },
};
```

---

## 다국어 플러그인 전역 설정 : main.js

#### > src / main.js

```javascript
import { createApp } from "vue";

import i18nPlugin from "./plugins/i18n"; // i18n 플러그인 추가
// 다국어 번역 데이터
const i18nStrings = {
  en: {
    hi: "Hello!",
  },
  ko: {
    hi: "안녕하세요!",
  },
};

const app = createApp(App);
app.use(i18nPlugin, i18nStrings); // i18n 플러그인에 다국어 번역 데이터를 파라미터로 전달 = options
app.mount("#app");
```

---

## 컴포넌트에서 다국어 플러그인 사용하기

전역설정까지 완료했다면 이제 모든 컴포넌트에서 다국어 플러그인을 사용할 수 있다.

#### > src / views / pluginView.vue

```html
<template>
  <h1>{{ '{{ $translate("en.hi") ' }}}}</h1>
  <!-- 화면 출력 : Hello! -->
</template>
```

---

## + provide / inject 로 플러그인 사용하는 방법

#### > src / plugins / i18n.js

```javascript
export default {
  install: (app, options) => {
    app.provide("i18n", options); // i18n key로 다국어 데이터 전달
  },
};
```

#### > src / views / pluginView.vue

```html
<template>
  <h1>{{ '{{ i18n.en.hi ' }}}}</h1>
</template>
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
