---
layout: post
title: Vue.js | Lifecycle Hooks
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI 5

<p align='center'><img width="70%" alt="스크린샷 2022-06-24 오후 10 31 03" src="https://user-images.githubusercontent.com/76654131/175546221-8585d594-9488-4499-8ab2-7b9d976a4b74.png">
</p>

---

## Lifecycle Hooks 기본 구조

```javascript
// <script>
export default {
  components: {},
  data() {},
  //props: {},

  // 제일 먼저 호출
  setup() {},

  // 인스턴스가 초기화되면 props 설정을 처리한 후 data() 또는 computed 같은 다른 옵션을 처리하기 직전에 호출
  beforeCreate() {},

  // data(), watch, computed, methods 이런 정보를 모두 가지고 준비가 끝난 상태
  created() {},

  // 반응 상태 설정을 완료를 했지만, 아직 DOM 노드가 생성되지 않은 상태.
  beforeMount() {},

  // 실제 DOM이 랜더링이 끝난 상태
  mounted() {},

  // data 변경으로 인해 DOM을 업데이이트 하기 직전 상태.
  beforeUpdate() {},

  // DOM이 업데이트 된 후에 호출
  updated() {},

  // 현재 컴포넌트를 빠져 나가기 직전
  beforeUnmount() {},

  // 현재 컴포넌트를 빠져 나갈 때
  unmounted() {},
};
```

---

## TIP 1

아래 코드처럼 `mounted` 시점에 데이터를 불러오는 함수를 정의해주면 `실제 DOM이 랜더링이 끝난 상태`이기 때문에 화면에 잘 출력이 될 것이다.

```javascript
  // 실제 DOM이 랜더링이 끝난 상태
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
        // 서버에 데이터를 요청.
        // 서버 DB에서 가져오는데 시간이 소요됨.
    }
  },
```

❗️ 그런데 사용자에게 보여줘야 할 `화면 상단 첫 부분`에 필요한 데이터를 서버에서 가져오는데 <font color='red'>시간이 좀 오래 걸린다고 </font> 가정하자.

그러면 사용자가 페이지에 접속했을 때 데이터 반영이 뒤늦게 되는 등 매끄럽지 못한 상황이 발생할 수 있다.

✔️ 이런 경우 `created` 시점에 데이터를 불러오는 함수를 정의해주면 `데이터가 미리 준비된 상태`로 mounted가 되기 때문에 문제가 해결될 것이다.

```javascript
// data(), watch, computed, methods 이런 정보를 모두 가지고 준비가 끝난 상태
  created() {
    this.getData()
  },
```

하지만 그렇다고 `created` 시점에 모든 함수들을 때려박으면 오히려 화면에 렌더링 되는 속도가 느려져 사용자가 잠시 빈화면을 보는 경우가 발생할 수 있으니 `화면 상황에 따라 적절하게 분배`해야 한다.

🔗 **사용자가 보는 입장에서의 렌더링 속도를 고려한 부분이다.**

---

## TIP 2

아래 코드에서 예시로 든 setInterval() 함수처럼 계속 실행되는 화면이 있다고 가정하자.

```javascript
// 실제 DOM이 랜더링이 끝난 상태
  mounted() {
    this.fnInterval = window.setInterval(() => {
      console.log('aaaa')
    }, 1000)
  },
```

❗️ 그런데 사용자가 이 화면, 즉 현재 컴포넌트를 빠져나가서 다른 페이지로 이동을 해도 **<mark style='background-color: #dcffe4'>Vue</mark>**는 `SPA(Single Page Application)`이기 때문에 계속 setInterval() 함수가 계속 반복해서 작동을 하고 있는 상태가 되어버린다.

✔️ 이런 경우 `현재 컴포넌트를 빠져 나가는` `unmounted` 시점에 함수를 종료해주면 성능면에서 좋게 해결된다.

```javascript
  // 현재 컴포넌트를 빠져 나갈 때
  unmounted() {
    window.clearInterval(this.fnInterval)

    // 참고) 아래처럼 안해줘도 큰 문제는 없겠지만 메모리를 생각하는 생각과 습관을 기르자.

    // 메모리 블럭에서 빠르게 가비지 컬렉션 대상이 되게끔 null 해주는게 좋음.
    // (이렇게 안해줘도 안쓰고 있으면 언젠간 가비지 컬렉션에서 정리해주긴 함.)
    this.fnInterval = null
    // getData - 서버에서 가져온 데이터 [] : 힙메모리로 메모리 블럭에 잡힌다.
    this.getData = null
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
> [https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram](https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)
