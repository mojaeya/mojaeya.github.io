---
layout: post
title: 배열은 왜 0부터 시작할까?
category: CS
tags: [CS]
comments: true
---
<br>
처음 프로그래밍 언어를 접했을때, 배열의 첫번째는 0이라는 사실을 그냥 받아들이고 넘어갔었다. 
왜 0부터 시작하는지에 대해 알아보자. 

### 컴퓨터 과학자들이 즐겨 쓰는 관습

### <font color="black"><center>"Half-open interval : 인덱스는 시작 수는 포함하고 마지막 수는 제외한다.<br> Zero-based numbering : 첫번째 인덱스는 0부터 시작한다."</center></font>

---

### 그래서 왜 0부터 시작하냐고요~
 
 
배열은 메모리에 순차적으로 공간을 차지한다.   
그렇다면 주소값이 있어야 하는데 그 **주소값은  맨처음에 위치**한다.   
**주소값 = 배열이 저장된 메모리의 시작 위치이라고 생각하면 쉽다.**
 
**주소값=시작** 위치를 기준으로 몇 칸이나 떨어져 있는지에 따라 인덱스에 해당하는 값을 가져오는거다.
 
그래서 첫번째 값은 주소값에서 1칸 떨어진게 아니고, 바로 그자리에서 가져오기 때문에 **인덱스는 0부터 시작**하는것이다.
 
---

### 더 쉽게 이해해보자.
 
<mark style='background-color: #dcffe4'>(주소값 + 할당값의 바이트 크기 * 인덱스 수)</mark> 이 공식으로 배열의 위치를 참조해 값을 가져올 수 있다.
 
- 첫번째 값을 가져오려면 주소값이 1000이라면 4byte * 0 = 0 이므로 주소값이 1000에 접근해서 값을 가져오고
- 두번째 값을 가져오려면 주소값이 1000이니깐 4byte * 1 = 4 이므로 주소값이 1004에 접근해서 값을 가져온다.

만약 인덱스가 1부터 시작한다면 첫번째 위치를 제대로 찾지 못할 수 있다.   
0부터 시작해야 첫번째 위치=주소값이 이동하지 않고 정확히 찾을 수 있는것이다.

```javascript
// javascript
const arr = new Array(4);
arr[0] = 1;
arr[1] = 2;
arr[2] = 3;
arr[3] = 4;

console.log(arr) // [1, 2, 3, 4]
```

이제 이 코드를 그냥 무식하게 받아들이는게 아니고 이유를 알고 보니 신선하네~

---

### 그 외 다른 이유들
- 메모리 주소는 0부터 시작한다.
- 인덱스가 1부터 시작하면 0이라는 공간을 낭비하게 되기 때문에.
- 컴퓨터가 계산하기 편하라고
- 다익스트라의 노트 => 난 이해를 못했다.

<br>

생각해보면,   
10진수도 0 ~ 9   
2진수도 0 ~ 1 

<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://get6.github.io/others/2020/why-index-start-zero/](https://get6.github.io/others/2020/why-index-start-zero/)   
[https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=dssh87&logNo=221363584443 ](https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=dssh87&logNo=221363584443)