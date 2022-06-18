---
layout: post
title: HTML 폼(form) 자식 태그 (datalist)
category: HTML
tags: [html]
comments: true
---

## <form> 의 자식태그

```html
<button> : 클릭 가능한 버튼이다. 기본 type은 submit이다.

<input> : 22가지 type을 지원한다. 기본 type은 text이다.

<label>	: <form>에 '라벨'을 달아주는 역할이다.
<!-- <label> 의 for 속성과 <input> 의 id 속성이 서로 같거나 <label>의 자식으로 <input>을 두어야 한다.
<input>에 focus가 오면 스크린리더가 <label>을 읽기 때문에 접근성 측면에서 중요하다. -->

<select> : <option>의 드랍다운을 만들어준다. 기본값으로 가장 첫번째 <option>이 선택되며 직접 입력은 불가능하다.
size 속성으로 드랍다운이 아니라 한 번에 여러 개를 보여주는 스크롤로 만들 수 있다.

<optgroup> : <select>를 카테고리별로 묶을 수 있다.

<datalist> : <option>의 드랍다운을 만들어준다. 검색기록 자동완성과 같이 직접 입력이 가능하다.
<!-- <datalist> 의 id 속성과 <input> 의 list 속성이 서로 같아야 한다. -->

<option> : 드랍다운 리스트에 어떤 옵션을 담을지 정의한다. value 속성을 가진다.

<fieldset> : <form> 에서 관련 요소를 그룹화할 때 사용한다. 관련 요소 주위에 상자를 그려준다.

<legend> : <fieldset> 요소 첫번째 자식으로 <fieldset> 그룹을 설명하는 캡션 역할을 한다.

<output> : <form>의 oninput속성에 있는 계산을 수행하고 결과를 <output> 요소에 표시한다.

<textarea> : 여러 줄을 입력할 수 있는 텍스트필드이다. rows 속성은 몇 줄 보일지를, cols 속성은 너비를 지정해준다.
```

---

## datalist 태그

- `<datalist>`는 `<input>` 요소에서 사용하기 위한 옵션들의 리스트를 미리 정의할 때 사용한다.

#### > `<select>` 요소는 사용자가 `<input>` 요소에 데이터를 입력할 수 없는 반면,

```html
<label for="city">살고있는 지역은?</label>
<select name="" id="city" value="">
  <option value="1">서울</option>
  <option value="2">부산</option>
  <option value="3">대전</option>
  <option value="4">대구</option>
  <option value="5">광주</option>
  <option value="6">제주</option>
</select>
```

<img width="168" alt="살고있는 지역은?, 지역 선택 박스" src="https://user-images.githubusercontent.com/76654131/166139264-07b4d245-f645-4432-935b-97b022d53553.png">
<img width="189" alt="살고있는 지역은?, 지역 드롭 리스트" src="https://user-images.githubusercontent.com/76654131/166139266-b401eb03-a1fe-4e97-be81-01d79565ea24.png">

#### > `<datalist>` 요소는 사용자가 `<input>` 요소에 데이터를 입력할 수 있고,<br>미리 정의된 옵션을 드롭다운 리스트로 보여줌으로써 `자동완성 기능`을 제공한다.

```html
<div>
  <input list="browsers" />
  <datalist id="browsers">
    <option value="Internet Explorer">Internet Explorer</option>
    <option value="Firefox">Firefox</option>
    <option value="Chrome">Chrome</option>
    <option value="Opera">Opera</option>
    <option value="Safari">Safari</option>
  </datalist>
</div>
```

<img width="222" alt="선택박스, 브라우저 드롭 리스트" src="https://user-images.githubusercontent.com/76654131/166139269-06ba4577-8cdf-48bc-a52e-cd8772447678.png">
<img width="163" alt="검색가능한 박스" src="https://user-images.githubusercontent.com/76654131/166139272-eaab0602-cdae-4893-a834-6905add98e5a.png">

<br>

한국인이라면 국가를 고를 때 어떤 웹사이트는 South Korea, 어떤 곳은 Republic of Korea라고 명시해 놓아서 스크롤을 왔다 갔다 하면서 찾은 경험이 있을 것이다.

이런 경우 `<datalist>`로 구성되어 있으면 검색해서 바로 찾을 수 있어 유용하다.

하지만 위에 그림과 같이 ch로 chrome을 쉽게 찾을 수 있지만, 선택을 제대로 하지 않고 input 요소에 ch만 입력해도 데이터가 그대로 전송되는 단점이 있다.  
(최종적으로 input에 입력되는 값이 옵션 목록에 있는 값과 맞는지 체크해 주는 자바스크립트 로직 프로그램을 따로 설정해 줘야 하는 이중 작업이 필요하다.)

#### > input 태그 요소의 list 속성값으로 datalist 태그 요소의 id 속성값을 명시하면,<br>해당 datalist 태그 요소에서 미리 정의한 옵션들을 input 태그 요소에서 사용할 수 있다.

```html
<div>
  <input list="browsers" id="broswer1" />
  <datalist id="browsers">
    <option value="Internet Explorer">Internet Explorer</option>
    <option value="Firefox">Firefox</option>
    <option value="Chrome">Chrome</option>
    <option value="Opera">Opera</option>
    <option value="Safari">Safari</option>
  </datalist>
</div>
<div>
  <input list="browsers" id="broswer2" />
</div>
<div>
  <input list="browsers" id="broswer3" />
</div>
```

만약 고객이 한 명 추가될 때마다 해당 국가를 추가해 줘야 하는 상황이라고 생각해 보자.
`<select>`로 구현을 하면 고객 수만큼 공통 옵션을 가진 **select 박스**가 추가되니
귀찮을 뿐만 아니라 태그가 많아지면 많아질수록 <font color="red">메모리도 많이 차지하고 로드 리스트가 느려진다.</font>

하지만 위에 코드처럼 `<datalist>`를 사용하면, 공통 옵션이 한 군데에만 있고 필요한 곳에는 input 태그만 간단하게 써주면 되기 때문에 <font color="#1E90FF">메모리도 훨씬 적게 잡아먹고 로드 리스트가 빨라진다.</font>

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [개발자의품격](https://www.youtube.com/c/개발자의품격)  
> [https://365kim.tistory.com/64](https://365kim.tistory.com/64)
