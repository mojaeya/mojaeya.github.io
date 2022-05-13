---
layout: post
title: CSS 박스 모델과 사이징
category: CSS
tags: [css]
comments: true
---

## 박스 모델 ( Box Model )

#### # 박스 개요

HTML 문서의 구성요소들은 기본적으로 `박스` 모양으로 정의된다.  
**CSS 박스 모델**은 `콘텐츠(Content)`, `패딩(Padding)`, `테두리(Border)`, 그리고 `마진(Margin)` 네 가지 요소로 구성된다.

<p align='center'><img width="417" alt="스크린샷 2022-05-13 오후 3 21 58" src="https://user-images.githubusercontent.com/76654131/168223215-4d2e3edd-f665-4f05-8be0-90fc9f6e48b4.png"></p>

- Contents box - 콘텐츠 영역으로 텍스트 및 이미지의 실제 영역.
- Padding box - Content를 둘러싼 공간(Border와 Content 사이의 공간)
- Border box - Content와 Padding을 둘러싼 선
- Margin box - Border를 둘러싼 공간

---

## 박스 크기 ( Box Sizing )

박스요소에 크기를 지정하면 기본적으로 콘텐츠 영역에 적용 된다.  
<font color='red'>그러나,</font> `실제 박스의 크기`는 <u>border, margin, padding을 모두 더해야 하기 때문에</u> 각각의 박스를 적절하게 배치 하려면 이들 크기가 함께 고려 되어야 한다.

```html
<style>
  div {
    width: 300px;
    height: 100px;
    padding: 10px;
    border: 10px solid green;
    margin: 10px;
  }

  .box-cb {
    box-sizing: content-box; /* 콘텐츠 크기 기준으로 width, height 적용  */
  }

  .box-bb {
    box-sizing: border-box; /* border까지 포함해서 width, height 적용 */
  }
</style>
<!-- <body> -->
<div class="box-cb">contetn-box</div>
<div class="box-bb">border-box</div>
```

<img width="369" alt="스크린샷 2022-05-13 오후 3 52 37" src="https://user-images.githubusercontent.com/76654131/168227667-43b56fbd-eeaa-457a-9a2c-cf01a48f5e81.png">

- width: 300px; height: 100px; 은 콘텐츠 영역이 300 x 100 임을 의미한다.

그런데 위의 그림을 보면 box-sizing 값에 따라서 우리 눈에 보이는 UI 상의 이미지 크기 차이가 큰 것을 알 수 있다.

`content-box` : 순수 콘텐츠 박스 크기만 300 x 100 (border까지 포함해서 340x140 이 되어버린다!)

<img width="210" alt="스크린샷 2022-05-13 오후 3 49 58" src="https://user-images.githubusercontent.com/76654131/168227276-33bad0d7-8cda-47d1-8edc-87cf29a3f2a4.png">

`border-box` : border 너비 까지 포함해서 300 x 100 (콘텐츠 박스 크기가 자동으로 260x60)

<img width="208" alt="스크린샷 2022-05-13 오후 3 50 15" src="https://user-images.githubusercontent.com/76654131/168227314-238ac53e-e359-4ed9-a0e3-36c3ac574294.png">

- 그래서 실제로 박스 크기 계산을 편하게 하기 위해서는 `border` 를 기준으로 하는 것이 편하다.
- box-sizing 속성을 boder-box 로 지정하면 된다.
- 디폴트는 content-box.

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [https://dinfree.com/lecture/frontend/122_css_3.html#m2](https://dinfree.com/lecture/frontend/122_css_3.html#m2)
