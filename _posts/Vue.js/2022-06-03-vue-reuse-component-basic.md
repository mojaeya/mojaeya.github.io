---
layout: post
title: Vue.js | 재사용 컴포넌트 기본
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI 5

#### **<mark style='background-color: #dcffe4'>Vue</mark>**의 가장 큰 장점 중 하나는 `컴포넌트를 재활용`하는 것이다. 즉, 다른 컴포넌트에 import해서 사용가능하다는 말이다.

---

## 컴포넌트(Component)

`컴포넌트(Component)`는 조합하여 화면을 구성할 수 있는 블록을 의미한다. 쉽게 View, Data, Code의 세트라고 생각하면 된다. `컴포넌트`를 활용하면 화면을 빠르게 구조화하여 일괄적인 패턴으로 개발 할 수 있으며, 코드를 쉽게 이해하고 재사용할 수 있다.

**<mark style='background-color: #dcffe4'>Vue</mark>**에서 `컴포넌트`는 우리가 화면에서 보는 페이지 자체일 수도 있고, 페이지 내의 특정 기능 요소일 수도 있다.

그러므로 **<mark style='background-color: #dcffe4'>Vue</mark>**로 개발을 할 때 `컴포넌트 설계`를 어떻게 하는지가 중요하다.  
(동일한 기능을 가진 컴포넌트를 하나 만들어 여러 페이지에서 사용)

**<mark style='background-color: #dcffe4'>Vue CLI</mark>**로 프로젝트를 생성하면 src 폴더 안에 `components`, `views` 폴더가 있는데  
`views` 폴더에 우리가 페이지라고 부르는 화면 하나 하나에 해당하는 **<mark style='background-color: #dcffe4'>Vue 컴포넌트</mark>** 파일을 생성하는거고,  
`components` 폴더에는 **<mark style='background-color: #dcffe4'>다른 Vue 폴더</mark>** 에서 호출해서 공통으로 사용할 수 있는 **<mark style='background-color: #dcffe4'>Vue 컴포넌트</mark>**을 생성하고 관리하게 되는 것이다.

결국 사실 **<mark style='background-color: #dcffe4'>Vue 입장</mark>**에서는 모든 vue 파일이 내부적으로는 모두 동일한 구조를 가진 컴포넌트이지만, 개발자가 물리적으로 이렇게 폴더를 구분해서 효율적으로 관리한다고 보면 된다.

---

## 컴포넌트 안에 다른 컴포넌트 사용하기

> Vue 네이밍 룰
>
> - 파일명은 두단어 이상 합성어로 작성하기!
> - 그리고 views 폴더는 xxxView.vue 로 작성하기!

#### > src / components / PageTitle.vue

```html
<template>
  <h2>사라진 기억들에게</h2>
</template>
```

#### > src / views / PageView.vue

```vue
<template>
    <div>
        <PageTitle /> // 3.html에서는 import한 컴포넌트 이름을 이용해서 태그를 만들면 끝!
        // <page-title /> : 이렇게 쓸 수도 있음
        // <p-t />
    </div>
</template>

<script>
import PageTitle from '@/components/PageTitle.vue' // 1. PageTitle 컴포넌트를 import
// import PageTitle from '../components/PageTitle.vue'
export default {
  components: { PageTitle }, // 2. 현재 컴포넌트 템플릿에서 사용할 컴포넌트를 등록
  // 컴포넌트 이름을 다르게 쓰고 싶으면 components: { 'p-t': PageTitle }
```

이렇게 하면 `components / PageTitle.vue` 파일에 작성한 <mark style='background-color: #dcffe4'><h2>사라진 기억들에게</h2></mark>가  
`views / PageView.vue` 파일에 사용되어 페이지 화면에 렌더링 된다.

✔️ 만약 공동으로 개발을 할 때 이렇게 페이지마다 각 타이틀에 대한 컴포넌트를 만들어 제공해서 사용한다면, 모든 화면에 대한 통일성을 가져갈 뿐 만 아니라 수정도 한번에 가능하기 때문에 효율적이다.

---

## `props` : 부모 컴포넌트에서 자식 컴포넌트로 데이터 전달

🔗 위에서 봤던 PageTitle.vue 파일을 아래와 같이 수정

#### > src / components / PageTitle.vue (자식 컴포넌트)

```vue
<template>
  <h3>{{ '{{ title ' }}}}</h3>
</template>

<script>
export default {
  // props에 title이라는 키를 갖는 객체를 추가
  props: {
    title: {
      type: String, // 저장될 데이터의 타입
      default: '페이지 제목' // 부모 컴포넌트로부터 데이터가 전달되지 않았을 때
    }
  },
```

`props`에는 `부모 컴포넌트`로 전달받은 데이터가 저장된다.  
`props`에 정의된 `Key`에는 저장될 데이터의 `type`과 `부모 컴포넌트`로부터 데이터가 전달되지 않았을 때의 `default` 값을 정의한다.

```html
<h3>{{ '{{ title ' }}}}</h3>
```

`props`에 정의된 `Key`는 **<mark style='background-color: #dcffe4'>Vue 인스턴스의 데이터 값</mark>**으로 사용되기 때문에 `{{ "{{ " }}}}` 콧수염 괄호(Mustache Tag)로 문자열에 대한 데이터 바인딩 처리가 가능하다.

---

🔗 PageView.vue 파일에서 사용하고 있는 PageTitle 컴포넌트에 title이라는 속성 추가

#### > src / views / PageView.vue (부모 컴포넌트)

✓ 여기서 설정한 title 값이, `자식 컴포넌트인` PageTitle.vue에 정의된 props의 title에 전달되는 것이다.

```html
<PageTitle title="사라진 기억들에게" />
```

---

## v-bind로 자식 컴포넌트 prop에 값 전달

#### ❗️ v-bind를 사용하지 않으면 문자열은 상관없겠지만 나머지 자료형들이 문자열로 전달되기 때문에 v-bind를 사용해야 한다!

#### 부모 컴포넌트

```vue
<template>
  <div>
    <child-component
      :str="strParent" <!-- 문자열(String) 전달 -->
      :num="numParent" <!-- 숫자형(Number) -->
      :isOk="isOkParent" <!-- 논리 자료형(Boolean) -->
      :arr="arrParent" <!-- 배열(Array) -->
      :obj="objParent" <!-- 객체(Object) -->
    />
  </div>
</template>

<script>
import ChildComponent from '@/components/ChildComponent.vue'
export default {
  components: { ChildComponent },
  data() {
    return {
      strParent: '사라진 기억들에게',
      numParent: 22,
      isOkParent: true,
      arrParent: [1, 2, 3, 4, 5],
      objParent: { name: 'mojaeya' }
    }
  },
}
```

---

## prop 유효성 검사

자바스크립트는 컴파일 시점이 아닌 런타임 시점에 모든걸 처리하기 때문에 어떤 값을 넣어도 에러가 뜨질 않는다.

그래서 props를 통해 전달받는 데이터에 대한 요구사항을 지정해주면, 컴포넌트를 사용하는 개발자가 어떤 타입으로 전달받게 코드를 작성해야 할지를 명확히 알고 개발을 하는 장점이 있다.

`자식 컴포넌트`에서 <mark style='background-color: #dcffe4'>props 옵션을 정의</mark>하는데는, `부모 컴포넌트`로부터 전달받는 데이터의 `type`, 데이터가 전달되지 않았을 때의 `default` 값, 필수여부 `required`, 유효성 검사 함수 `validator` 등이 있다.

```javascript
// 기본 타입 체크 ("null" 과 "undefined"는 모든 타입 유효성 검사를 통과한다.)
  props: {
    str: {
      type: String,
      default: ''
      required: true // 부모 컴포넌트로부터 반드시 데이터가 필수로 전달되어야 함.
    },
    num: {
      type: Number,
      default: 0
    },
    isOk: {
      type: Boolean,
      default: false
    },

    // 객체나 배열의 기본값(default)은 항상 팩토리 함수로부터 반환되어야 한다.
    // new를 붙여 호출하는 생성자함수(Constructor)를 통해 만든 함수가 아닌것을 '팩토리함수'라고 부른다.
    arr: {
      type: Array,
      default: function () {
        return []
      }
    },
    obj: {
      type: Object,
      default: function () {
        return {}
      }
    }

    // 그외

    // 커스텀 유효성 검사 함수
    propF : {
      validator: function(value) {
        // 값이 꼭 아래 세 문자열 중 하나와 일치해야 한다.
        return ['sucess', 'warning', 'danger'].indexOf(value) !== -1
      }
    },

    // 기본 값을 갖는 함수
    propG : {
      type: Function,
      default: function() { // 이건 팩토리 함수가 아니고 기본 값으로 사용되는 함수임!
        return 'Default function'
      }
    },
  },
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)
