---
layout: post
title: Vue.js | 데이터 바인딩 Data Binding
category: Vue.js
tags: [vue.js]
comments: true
---
> Vue.js 3.x / Vue-CLI

 **<mark style='background-color: #dcffe4'>Vue</mark>**는 **Angular**와 마찬가지로 `양방향 데이터 바인딩`을 지원한다. 그리고 **React**는 `단방향 데이터 바인딩`만을 지원한다.    
 일단 `양방향 데이터 바인딩`을 알아보기 전에 `단방향 데이터 바인딩`를 먼저 보고 가자. 

---

## 단방향 데이터 바인딩 (One-way binding) 

데이터 바인딩(Data Binding)은 뷰 인스턴스에서 정의한 속성들을 화면에 표시하는 방법이다.   
가장 기본적인 데이터 바인딩 방식은 `{{ "{{ " }}}}` 콧수염 괄호(Mustache Tag)이다. 

### 문자열 
```html
<!-- <template> -->
  <div>
    <p>{{ "{{ message " }}}}</p>
  </div>
```

```javascript
// <script>
export default {
  data() {
    return {
      message: '사라진 기억들에게'
    }
  }
}
```

div 태그에 `{{ "{{ " }}}}` 콧수염 괄호를 이용해  **<mark style='background-color: #dcffe4'>Vue 인스턴스</mark>**의 `message` 속성을 연결한 코드다.    
코드를 실행하면 화면에 '사라진 기억들에게' 라는 문자가 출력된다.

만약 바닐라 자바스크립트로 서버로부터 데이터를 가져와서 document.querySelector, innerText 등으로 출력해준다고 생각하면 대비 너무 편해졌다. (vue에서는 document 객체를 쓸일이 없다!)

이렇게 자바스크립트에서 HTMl 태그 쪽으로 한방향으로만 데이터 바인딩하는 것을 `단방향 데이터 바인딩`이라고 한다.

---

### HTML 

> 디렉티브는 Vue로 화면의 요소를 더 쉽게 조작하기 위한 문법이다.  v- 접두사 사용

실제 HTML로 출력되기 위해서 `v-html` 디렉티브 사용

```html
<!-- <template> -->
  <div>
     <div v-html="htmlString"></div>
  </div>
```

```javascript
// <script>
export default {
  data() {
    return {
       htmlString: '<p style="color:red;">빨간색 문자</p>'
    }
  }
}
```

---

## 양방향 데이터 바인딩 (two way binding)

### Form 입력 
`v-model` 디렉티브 사용
```html
<!-- <template> -->
  <div>
     <input type="text" v-model="userId" />
  </div>
```

```javascript
// <script>
export default {
  data() {
    return {
      userId: 'mojaeya'
    }
  }
}
```

input type=text 에서 `v-model`은 내부적으로 input type=text의 `value` 속성을 사용한다.  

data()에 정의된 데이터 키명(userId)을 v-model에 넣어주면 `모델인 data`와 `뷰인 input type=text의 value 속성`이 서로 `양방향 데이터 바인딩`이 설정되는 것이다. 

실제로 사용자가 입력폼의 값을 `변경`하면 별다른 코드 작성 없이도 `변경된 데이터`가 실시간으로 `모델인 data의 useId에 그대로 저장`이 된다. 

> v-model.number  - 숫자로 변환

---

### Select 
Select 객체 역시 input type=text와 동일하게 `v-model`은 내부적으로 select의 `value` 속성을 사용해서 `양방향 데이터 바인딩`을 한다.

```html
<!-- <template> -->
  <div>
    <select v-model="selectedCity">
      <option value="02">서울</option>
      <option value="051">부산</option>
      <option value="064">제주</option>
    </select>
  </div>
```
```javascript
// <script>
export default {
  data() {
    return {
       selectedCity: '051'
    }
  }
}
```

--- 

### Checkbox 
체크박스는 input type=text,select와 다르게 `v-model`이 내부적으로 체크박스의 `checked` 속성을 사용한다.   

바닐라 자바스크립트에서 name 속성 값을 똑같이 해주면 하나의 그룹으로 묶이는 것과 같이  **<mark style='background-color: #dcffe4'>Vue</mark>** 에서는 아래 코드와 같이 v-model에 바인딩된 속성 값이 똑같으면 하나의 그룹으로 엮인다.

```html
<!-- <template> -->
<div>
    <div>
      <input type="checkbox" id="html" value="HTML" v-model="favoriteLang"/>
      <label for="html">HTML</label>
    </div>
    <div>
      <input type="checkbox" id="css" value="CSS" v-model="favoriteLang"/>
      <label for="css">CSS</label>
    </div>
    <div>
      <input type="checkbox" id="js" value="JS" v-model="favoriteLang"/>
      <label for="js">JavaScript</label>
    </div>
</div>
```
```javascript
// <script>
export default {
  data() {
    return {
        favoriteLang: [] // 여러 개의 체크박스를 사용할 때는 배열 []을 사용해야 한다.  radio의 경우 문자열 ''
    }
  }
}
```
앞서 `v-model`이 내부적으로 체크박스의 `checked` 속성을 사용한다고 했기 때문에,   
만약 `value 속성에 데이터 바인딩`을 하려면 v-model이 아닌 `v-bind:value`을 사용해야 한다.
 
---

## v-bind - 단방향 데이터 바인딩 (One-way binding) 

### 속성(Attribute)

아래와 같이 readonly를 하는 텍스트는 굳이 v-model을 쓸 필요가 없다. 오히려 자바스크립트 조작으로 위험할 수 있기 때문이다.
이런 경우 value 속성에 직접 단방향 데이터 바인딩을 해버리는 것이 낫다.

#### readonly
```html
<!-- <template> -->
  <div>
    <input type="text" name="" id="" v-bind:value="userId" readonly />
    <input type="text" name="" id="" :value="userId" readonly /> <!-- v-bind 생략 가능! -->
  </div>
```

#### img 객체의 src
```html
<!-- <template> -->
  <div>
    <img :src="imgSrc"/>
  </div>
```
```javascript
// <script>
export default {
  data() {
    return {
        imgSrc: "url"
    }
  }
}
```

#### disabled
사용자가 입력폼에 입력을 해야만 조회 버튼이 활성화되게 설정
```html
<!-- <template> -->
  <div>
    <input type="text" name="" id="" v-model="txt1" />
    <button :disabled="txt1 === ''">조회</button>
  </div>
```
```javascript
// <script>
export default {
  data() {
    return {
        txt1: ''
    }
  }
}
```

---

### 클래스 바인딩
위에서 봤던 속성의 경우 하나의 속성만을 이용해서 바인딩해야 하지만,   
클래스는 기본 클래스와 데이터 바인딩 처리를 하는 클래스를 공존해서 사용 가능하다.

#### 클래스 바인딩은 Object 형태로 사용하며, 바인딩할 클래스를 key로 잡고 바인딩 여부를 true/false로 지정한다.
```html
<!-- <template> -->
  <div>
    <div class="container" v-bind:class="{ 'text-red': hasError, active: isActive }">클래스 바인딩</div>
    <div :class="class2">클래스 바인딩2</div>
  </div>
```
```javascript
// <script>
export default {
  data() {
    return {
        isActive: false,
        hasError: false,
        class2: ['active', 'hasError'] // 이렇게 배열 형태로 할당할 수 있는데 이 경우 true/false 클래스 바인딩 처리 불가능 
    }
  }
}

// <style scoped>
.container {
  width: 100%
  height: 200px;
}

.active {
  background-color: greenyellow;
  font-weight: bold;
}

.text-red {
  color: red;
}
```

---

### 인라인 스타일 바인딩
인라인 스타일은 데이터를 Object로 선언해서 바인딩 할 수 있다.
(클래스 바인딩처럼 배열을 이용해 바인딩 처리 가능)

```html
<!-- <template> -->
    <!-- 일반 HTML 인라인 스타일 적용 방식 -->
    <!-- <div style="color: red; fontsize: 30px"> 스타일 바인딩: 글씨는 red, 폰트크기: 30px </div> -->
  <div>
    <div :style="style1">스타일 바인딩: 글씨는 red, 폰트크기: 30px</div>
  </div>
```
```javascript
// <script>
export default {
  data() {
    return {
        style1: {
        color: 'green',
        fontSize: '30px' // 대문자 주의
      }
    }
  }
}
```


<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [Vue.js 프로젝트 투입 일주일 전](http://www.yes24.com/Product/Goods/101926719)   
> [캡틴판교](https://joshua1988.github.io/vue-camp/vue/template.html#데이터-바인딩)
