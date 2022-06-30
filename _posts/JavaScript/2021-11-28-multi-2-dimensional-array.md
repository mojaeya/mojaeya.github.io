---
layout: post
title: JavaScript | 다차원 배열과 유사 배열
category: JavaScript
tags: [javascript, 모던 JS 입문]
comments: true
---

#### [ JAVA ] 2차원 배열의 선언

```
int [][] array; // 2차원 배열의 선언

array = new int[1][5];   // 2차원 배열의 초기화
```

#### <font color='red'>but</font> 자바스크립트의 2차원 배열이란?

- 자바스크립트는 기본적으로 2차원 배열을 지원하지 않는다
- const arr = \[\]\[\] 이와 같은 2차원 배열 선언이 불가능하다.
- 약간의 트릭을 이용하여 2차원 배열과 비슷한 배열을 만들 뿐이다. (배열안에 배열을 넣는 방식)

#### [ JavaScript ] 2차원 배열의 선언

```javascript
// arr[5][2]    // 초기값을 할당하여 배열 생성
let arr = [
  ["a", "b"],
  ["c", "d"],
  ["e", "f"],
  ["g", "h"],
  ["i", "j"],
];

// arr[5][2]    // 반복문을 사용하여 빈 배열 생성
let arr = new Array(5);

for (let i = 0; i < arr.length; i++) {
  arr[i] = new Array(2);
}
```

---

## 다차원 배열  ( 2차원 배열 이상 )

다차원 배열은 배열 내부의 요소로 배열을 추가하면 된다 = 배열의 요소로 다른 배열이 들어가는 것

```javascript
let num = [10, 20, ["가", "나", "다", "라"], "a", "b", "c"];
console.log(num[1]); //  20
console.log(num[2]); //  ['가','나','다','라']
// 배열 num의 2번째의 인덱스는 ['가','나','다','라'] 라는 '배열'이 '값'으로 나온다.
// 해당 배열의 인덱스에도 접근이 가능하다.

// 두번째 배열의 인덱스 값은 '배열'이 아닌 '요소'가 출력된다.
console.log(num[2][0]); //  가
```

첫번째 배열 'num'의 인덱스 값 \[2\]를 넣으면 \['가','나','다','라'\] 배열이 나오고,

첫번째 배열의 인덱스 값 옆에 두번째 배열의 인덱스 값\[0\]을 넣으면,

두번째 배열 \['가','나','다','라'\]의 0번째 인덱스 값인 '가' 출력.

_\=> 이 때 출력된 인덱스 값은 배열이 아닌 '가'라는 요소로 나온다. 이를 `다차원 배열, 중첩된 배열` 이라고 한다_

---

**`유사배열을 알아보기 전에!`**

**자바스크립트에서 배열이란?**  곧 Array 타입의 객체를 말한다. Array 타입의 객체는 다음과 같은 성질이 있다.

- 0 이상의 정수 값을 프로퍼티 이름으로 갖는다
- length 프로퍼티가 있으며, 요소를 추가하거나 삭제하면 length 프로터티 값이 바뀐다. 또한 length 프로퍼티 값을 줄이면 그에 따라 배열 크기가 줄어든다.
- 프로토타입이 Array.prototype 이므로 Array.prototype의 메서드를 상속 받아서 사용할 수 있다. 또한 instanceof 연산자로 평가하면 Array 생성자 함수로 생성된 객체로 표시된다.

---

## 유사배열

```javascript
let array = [1, 2, 3];
array; // [1, 2, 3]

let nodes = document.querySelectorAll("div"); // NodeList [div, div, div, div, div, ...]
let els = document.body.children; // HTMLCollection [noscript, link, div, script, ...]
```

위 예제에서 array는 `배열`이고, nodes와 els는 `유사배열`이다. 다 []로 감싸져 있어서 겉만 봐서는 구분하기가 힘들다

배열인지 판단해주는 `Array.isArray` 메서드를 사용해보면,

```javascript
Array.isArray(array); // true    => 직접 배열 리터럴로 선언한 array만 배열이다.
Array.isArray(nodes); // false
Array.isArray(els); // false
```

**`유사배열은 배열처럼 보이지만 사실 배열의 성질 중 프로퍼티 이름 즉, key가 숫자(0이상의 정수)이고 length 프로퍼티를 가지고 있는 객체를 말한다.`**

( 참고로 string도 유사배열이다. length property를 가지며, 0부터 index로 접근할 수 있기 때문이다. )

```javascript
let ArrayLikeObject = {
  0: "a",
  1: "b",
  2: "c",
  length: 3,
};
```

위에 코드에 나온 객체가 **`유사 배열`**이다. 그래서 **`유사배열 객체`**라고도 부른다. ( key가 숫자고, length라는 프로퍼티도 가지고 있다. )

사실 배열도 객체라는 성질을 이용한 트릭이기 때문에 배열처럼 유사배열도

ArrayLikeObject\[0\], ArrayLikeObject\[1\], ArrayLikeObject.length 같은 것을 모두 사용 가능하다.

---

#### <font color='red'>but</font> `배열`과 `유사배열`을 구분해야 하는 이유!  => `유사배열은` <font color='red'>배열의 메서드(Array.prototype의 메서드)를 사용 못한다.</font>

그런데 유사배열도 배열의 메서드를 빌려 쓰는 방법이 있긴 하다.

바로 Function.prototype.**call 메서드**로 간접 호출하면 사용 가능하다.

```javascript
let a = { 0: "A", 1: "B", 2: "C", length: 3 };

Array.prototype.push.call(a, "D");
// object {0: 'A', 1: 'B', 2: 'C', 3: 'D', length: 4}

Array.prototype.slice.call(a, 0); //
// ['A', 'B', 'C', 'D'] => 진짜 배열로 변환해서 반환
```

#### **ES6 부터는 Array.from() 메서드로도 가능하다.**

> **Array.from() 메서드는 유사 배열 객체(array-like object)나 반복 가능한 객체(iterable object)를 얕게 복사해 새로운Array 객체를 만든다.**

```javascript
let a = { 0: 1, 1: 2, 2: 3, length: 3 };

Array.from(a).map(function (v) {
  return v * v;
}); // [1, 4, 9]
```

---

## 그럼 유사배열을 사용하는 이유는?

어떤 함수에서 실행 결과로 배열값을 돌려주고 싶을때, 원래의 배열 객체가 가지고 있는 기능(함수)를 제공하고 싶지 않거나,

원래의 배열 객체에 없는 기능을 제공하고 싶을때 유사배열을 사용한다.

즉 원래의 Array 와 다른 배열을 사용하고 싶을때 유사배열을 이용하는 것이다.

#### []로 감싸져 있다고 다 같은 배열이 아니라는거 명심하자!

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://www.zerocho.com/category/JavaScript/post/5af6f9e707d77a001bb579d2](https://www.zerocho.com/category/JavaScript/post/5af6f9e707d77a001bb579d2)  
> [https://gent.tistory.com/296](https://gent.tistory.com/296)
