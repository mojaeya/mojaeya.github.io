---
layout: post
title: CSS 포지셔닝
category: CSS
tags: [css]
comments: true
---

## CSS Position

`position` 속성은 박스 구성요소들을 배치하기 위한 속성이다. 어떤 `position` 속성을 사용 하느냐에 따라 위치가 달라질 수 있으므로 전체적인 내용을 잘 이해하고 익숙하게 사용할 수 있도록 해야 한다.

<p align='center'><img width="560" alt="스크린샷 2022-05-13 오후 6 29 05" src="https://user-images.githubusercontent.com/76654131/168254754-aa5f52d8-da27-4e45-97dd-80a6b81a9004.png">
</p>

### # static

- position 속성의 기본값으로 요소를 나열한 순서대로 배치 (원하는대로 배치 못함)

### # relative

- static과 같이 나열한 순서대로 배치되지만 top, right, bottom, left 속성을 사용해 원하는 위치를 지정할 수 있다.

```html
<style>
  .relative {
    position: relative;
    left: 30px;
    border: 3px solid red;
  }
</style>
<!-- <body> -->
<div class="relative">
  원래 자기 자신이 있어야 하는 위치에서 left:30px 만큼 오프셋됩니다.
</div>
```

### # absolute

- top, right, bottom, left 속성값을 이용해 요소를 원하는 위치에 배치할 수 있다.
- 이때 `기준 위치`는 가장 가까운 상위 요소 중 position 속성이 `relative`인 요소.
- 따라서 absolute를 사용하는 경우 콘텐츠 박스를 감싸는 컨테이너를 만들고 position을 relative로 지정해놓고 사용.
- 상위 요소가 없다면 브라우저 화면의 좌측상단을 기준으로 설정.

```html
<style>
  .relative {
    position: relative;
    width: 400px;
    height: 130px;
    border: 3px solid green;
  }

  .absolute {
    position: absolute;
    top: 80px;
    right: 10px;
    width: 240px;
    border: 3px solid red;
  }
</style>
<!-- <body> -->
<div class="relative">
  position:relative로 설정된 부모 요소
  <div class="absolute">postion:absolute로 설정된 요소</div>
</div>
```

<img width="427" alt="스크린샷 2022-05-13 오후 9 08 17" src="https://user-images.githubusercontent.com/76654131/168280014-277412e4-fb60-436a-bef6-1af08d1c440e.png">

### # fixed

- absolute 속성처럼 좌표로 위치를 결정하지만 기준이 부모요소가 아닌 브라우저 창(Browser Window).
- 페이지를 스크롤하더라도 계속 고정되어 표시된다. 즉, 항상 같은 위치를 유지.  
  ex) 글 한참 내리다가 버튼 누르면 위로 스르르륵 올라가는 기능이 필요한 경우

### # sticky

- 기준이 부모요소
- top과 left 같은 포지션을 지정해줘야 한다.
- 스크롤링 될 때 고정이 된다.

```html
<style>
  .sticky {
    position: sticky;
    top: 0;
    padding: 5px;
    background-color: greenyellow;
    border: 2px solid green;
  }
</style>
<!-- <body> -->
<h2>
  position:stick가 적용된 요소는 마우스 스크롤시 정의된 위치에 고정해줍니다.
</h2>
<div class="sticky">position:sticky 영역</div>
<div style="padding-bottom: 2000px">
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
  <p>콘텐츠</p>
</div>
```

![May-13-2022 21-11-30](https://user-images.githubusercontent.com/76654131/168280975-e754867b-0449-42c1-a4d8-d78580c805d0.gif)

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [https://dinfree.com/lecture/frontend/122_css_3.html#m2](https://dinfree.com/lecture/frontend/122_css_3.html#m2)
