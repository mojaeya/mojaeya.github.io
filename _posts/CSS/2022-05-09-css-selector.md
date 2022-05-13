---
layout: post
title: CSS 선택자
category: CSS
tags: [css]
comments: true
---

## CSS 선택자

- CSS에서는 스타일을 적용할 대상을 선택하기 위해서 선택자(selector)를 사용한다.

<p align='center'><img width="600" alt="스크린샷 2022-05-13 오후 12 05 10" src="https://user-images.githubusercontent.com/76654131/168203272-3f837451-b38a-44e7-9a46-2474282c907a.png"></p>

#### # 전체 선택자

- 전체 선택자는 HTML 페이지 내부의 모든 태그에 지정된 스타일을 적용

```html
<style>
  /* 전체 선택자 */
  * {
    color: red;
    background-color: greenyellow;
  }
</style>
```

#### # 클래스 선택자

- 클래스 선택자는 태그의 class 속성값을 활용하는 선택자

```html
<style>
  /* 클래스 선택자 */
  /* 선택자 이름이 점(.)으로 시작 */
  .color-red {
    color: red;
  }

  .bg-yellow {
    background-color: yellow;
  }
</style>
<!-- <body> -->
<p class="color-red">빨간 글자색입니다.</p>
<p class="color-red bg-yellow">빨간색 글자에 노란색 배경입니다.</p>
```

#### # 태그 선택자

- 태그 선택자는 태그명을 사용해서 HTML 요소를 찾고, 동일한 스타일 속성을 적용하기 위해 사용

```html
<style>
  /* 태그 선택자 */
  /* 태그 이름을 선택자로 사용 */
  a {
    text-decoration: none;
  }
</style>
```

> 하이퍼링크를 위한 태그인 `<a>` 태그는 원래 `<a>` 태그 안의 텍스트에 밑줄이 자동으로 추가되게 된다.<br> 태그 선택자 안에 text-decoration: none; 사용하면 밑줄이 사라지게 된다.

#### # ID 선택자

- ID 선택자는 태그가 id 속성 값이 <font color='red'>유일</font>하다는 특징을 활용한 선택자
  > HTML 태그에서 id는 모든 태그에서 사용할 수 있는 속성이며 반드시 중복되는 값이 없는 유일한 값을
  > 속성 값으로 사용해야 한다.

```html
<style>
  /* id 선택자 */
  /* # + id 속성 값 */
  #container {
    width: 400px;
    height: 50px;
    background-color: greenyellow;
  }
</style>
<!-- <body> -->
<div id="container"></div>
```

#### # 복합 선택자

<img width="600" alt="스크린샷 2022-05-13 오후 12 34 59" src="https://user-images.githubusercontent.com/76654131/168206243-f4ec72b3-a561-4c37-a1cf-5eeb4e3ec981.png">

<img width="700" alt="스크린샷 2022-05-13 오후 12 38 16" src="https://user-images.githubusercontent.com/76654131/168206544-05bab7d8-af1f-472a-9e40-0c0956728193.png">

#### # 속성 선택자

```html
<style>
  /* 속성 선택자 */
  /* E[attr] 형식 */
  a[href] {
    color: black;
    text-decoration: none;
  }

  /* E[attr="val"] 형식 */
  input[type="text"] {
    border: 2px solid red;
  }

  [name="blue"] {
    border: 2px solid blue;
  }
</style>
<!-- <body> -->
<a href="/link">링크</a>
<input type="text" name="" id="" />
<input type="email" name="blue" id="" />
<div name="blue">abc</div>
```

#### # 가상 클래스 선택자

- 가상 클래스 선택자는 특정 요소에 마우스가 포커스 되거나, 버튼 위에 마우스가 위치 되거나 하는 사용자의 이벤트에 대해 스타일을 지정하는 선택자이다.

| 가상 클래스 선택자 |               기능               |
| :----------------: | :------------------------------: |
|       :link        |      방문한 적이 없는 링크       |
|      :visited      |      방문한 적이 있는 링크       |
|       :hover       |     마우스를 롤오버 했을 때      |
|      :active       |       마우스를 클릭했을 때       |
|       :focus       | 포커스 되었을 때 (input 태그 등) |
|       :first       |           첫번째 요소            |
|       :last        |           마지막 요소            |
|    :first-child    |           첫번째 자식            |
|    :last-child     |           마지막 자식            |
|  :nth-child(2n+1)  |          홀수 번째 자식          |

#### `링크와 입력창에 활용`

```html
<style>
  /* 가상 클래스 선택자 */
  a {
    text-decoration: none;
  }

  /* 마우스가 오버 됐을때 */
  a:hover {
    color: red;
  }

  /* 방문한 적이 없는 링크 */
  a:link {
    color: blue;
  }

  /* 방문한 적이 있는 링크 */
  a:visited {
    color: green;
  }

  /* 마우스가 포커스 됐을 때  */
  input:focus {
    border: 5px solid red !important;
  }
</style>
<!-- <body> -->
<a href="https://naver.com">네이버</a>
<a href="https://google.com">구글</a>
<br />
<input type="text" name="" id="" />
```

#### `테이블에 활용`

```html
<style>
  table,
  th,
  td {
    border: 1px solid black;
    border-collapse: collapse;
  }

  table {
    width: 100%;
  }

  /* 홀수 행에만 색깔 적용 */
  tbody tr:nth-child(2n + 1) {
    background-color: greenyellow;
  }
</style>
<!-- <body> -->
<table>
  <thead>
    <tr>
      <th>이름</th>
      <th>연락처</th>
      <th>이메일</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>손흥민</td>
      <td>010-0000-0000</td>
      <td>son@email.com</td>
    </tr>
    <tr>
      <td>박지성</td>
      <td>010-0000-0001</td>
      <td>park@email.com</td>
    </tr>
    <tr>
      <td>차범근</td>
      <td>010-0000-0002</td>
      <td>cha@email.com</td>
    </tr>
  </tbody>
</table>
```

<img width="681" alt="스크린샷 2022-05-13 오후 1 02 17" src="https://user-images.githubusercontent.com/76654131/168208873-8c84f382-3a07-4aa2-9537-b19e477911c4.png">

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)
