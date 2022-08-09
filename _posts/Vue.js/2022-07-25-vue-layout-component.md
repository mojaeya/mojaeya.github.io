---
layout: post
title: Vue.js | 레이아웃 컴포넌트
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI

웹페이지는 여러 다양한 화면으로 구성되어 있지만,  
일반적으로 `상단(header)`에 로고와 메뉴, `가운데`에 컨텐츠 내용, `하단(footer)`에 사이트정보 등의 `고정적인 형태`로 화면이 반복되는 경우가 많다.

그렇기에 이번 포스팅에서는 이중에서도 항상 고정적인 `header` 영역과 `footer` 영역의 레이아웃 컴포넌트를 분리해서 사용하고자 한다.

---

일단 먼저 `Header`와 `Footer` 레이아웃 컴포넌트를 **components/layouts** 폴더에 따로 분리해서 만들어준다.

## Header 레이아웃 컴포넌트 생성

#### > src / App.vue

```html
<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
  </nav>
</template>
```

기존 `App.vue`에서 메뉴(네이게이션) 역할을 하던 코드 부분을 그대로 `Header` 레이아웃 컴포넌트로 복사한다.

#### > src / components / layouts / HeaderLayout.vue

```html
<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
  </nav>
</template>
```

---

## Footer 레이아웃 컴포넌트 생성

`Footer` 레이아웃 컴포넌트는 간단하게 부트스트랩 - Footers를 이용해서 작성해주었다.

#### > src / components / layouts / FooterLayout.vue

```html
<template>
  <div class="container">
    <footer
      class="d-flex flex-wrap justify-content-between align-items-center py-3 my-4 border-top"
    >
      <div class="col-md-4 d-flex align-items-center">
        <span class="mb-3 mb-md-0 text-muted">&copy; 2022 Company, Inc</span>
      </div>
    </footer>
  </div>
</template>
```

---

## 기본적인 레이아웃은 최상위 컴포넌트인 `App.vue`에서 모두 구성한다.

`App.vue`에서 **components/layouts** 폴더에 만들어둔 `Header`와 `Footer` 레이아웃 컴포넌트를 아래와 같이 import해서 재사용하면 된다.

#### > src / App.vue

```html
<template>
  <header-layout />
  <router-view />
  <footer-layout />
</template>
```

```javascript
// <script>
import HeaderLayout from "@/components/layouts/HeaderLayout.vue";
import FooterLayout from "@/components/layouts/FooterLayout.vue";
export default {
  components: { HeaderLayout, FooterLayout },
};
```

---

이렇게 되면 `Header`, `footer` 레이아웃은 모든 페이지에서 고정적으로 보여지게 되고,  
`Header` 레이아웃에 있는 메뉴를 클릭할 떄 마다 라우터가 변경되면서 해당되는 컴포넌트가 `router-view`를 통해 화면에 출력될 것이다.

> <br>
> <br>
> <br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
