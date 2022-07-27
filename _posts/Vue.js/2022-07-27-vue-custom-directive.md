---
layout: post
title: Vue.js | Custom Directive
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI

**<mark style='background-color: #dcffe4'>Vue</mark>**에서는 `v-model`, `v-show` 디렉티브 같은 기본 내장된 디렉티브 외에도 사용자가 직접 디렉티브를 정의해서 사용할 수 있다.

이번 포스팅에서는 사용자가 웹사이트 로그인 페이지에 접속하는 순간 바로 첫번째 입력 필드로 포커스 되도록 하는 `커스텀 디렉티브(Custom Directive)`를 만들어보자.

---

## v-focus 커스텀 디렉티브 생성

간단하게 부트스트랩 이용해서 로그인 페이지 폼을 구성해줬다.

```html
<template>
  <div>
    <div>
      <label for="email" class="form-label">이메일주소</label>
      <input type="email" name="" id="email" class="form-control" v-focus />
    </div>
    <div>
      <label for="pw" class="form-label">비밀번호</label>
      <input type="password" name="" id="pw" class="form-control" />
    </div>
    <div>
      <button class="btn btn-primary">로그인</button>
    </div>
  </div>
</template>
```

directives 옵션에 커스텀 디렉티브를 아래와 같이 정의해준다.

```javascript
// <script>
export default {
  components: {},
  directives: {
    focus: {
      mounted(el, binding) {
        el.focus(); // el -> element 약자로 현재 커스텀 디렉티브가 적용된 요소가 el로 들어오는 것이다.
        // binding ->  커스텀 디렉티브에 바인딩 값이 적용되어 있다면 binding.value 로 값 불러오기 가능
      },
    },
  },
};
```

컴포넌트가 `mounted` 되면 `v-focus` 디렉티브를 적용한 html 객체(예제에서는 이메일주소 입력창)로 포커스가 된다.

---

## 커스텀 디렉티브 전역 설정

위에서 특정 컴포넌트 안에서만 사용하도록 커스텀 디렉티브를 등록했는데, 전역에서 사용할 수 있게 하는 방법도 알아보자.

#### > main.js

```javascript
const app = createApp(App)
...
app.directive('focus', {
  mounted(el, binding) {
    el.focus()
  }
})
```

이렇게 main.js에 커스텀 디렉티르를 위와 같이 추가하면 전역에서 `v-focus` 디렉티브를 사용 가능하다.

---

여기서는 간단한 것만 다루었지만, 정규식 등을 이용해서 만든 `커스텀 디렉티브`를 잘 사용한다면 개발 생산성도 올라가고 매우 편리해질 것이다!

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
