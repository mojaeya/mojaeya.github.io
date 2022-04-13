---
layout: post
title: Signed vs UnSigned
category: CS
tags: [cs, computer architecture]
comments: true
---

<br>
>**Signed  : 부호를 가지는 값 ( 양수, 음수 구분 가능)**   
<br>
>**UnSigned : 부호를 가지지 않는 값 ( Only 양수)**

#### _✓ 쉬운 이해를 위해 8비트를 기준으로 정리한다._

<br>
▶︎ **Signed**  : 음수표현을 위해 2의 보수 체계 사용, 부호 구별하는 **MSB**(Most Significant Bit) = 최상단 비트 필요   
* MSB: 0 => 양수 MSB: 1 => 음수
<br>

▶︎ **UnSigned** : 부호가 없기 때문에 음수 표현 x, 대신 양수를 2배만큼 표현 가능
<br>

> **8비트 경우 Signed : -128 ~ 127 / UnSigned : 0 ~ 255**

<br>

이해를 위해 예를 들어보자.  
만약, (8비트)컴퓨터가 127이라는 수를 저장 한다면, 127을 이진수 변환하면 1111111

- **Signed** : 제일 앞 비트인 MSB를 하나 소비  
  <img width="70%"  src="https://user-images.githubusercontent.com/76654131/139401865-ed3dc939-3539-4b0b-8a5a-e11dee8d0f2b.png">

- **UnSigned**  
  <img width="70%" alt="스크린샷 2021-10-29 오후 5 24 35" src="https://user-images.githubusercontent.com/76654131/139401900-50770750-39c9-448c-a5f2-b890c00c5f20.png">

<br>
### 그럼 -128을 저장하면?  
일단 먼저,<u>컴퓨터는 음수를 처리할 때 2의 보수법을 사용한다는것을 명심하자.</u>

### 보수?

```shell
보수란, '두 수의 합이 진법의 밑수(N)가 되게 하는 수'를 말한다.

예를 들어 10진수 4의 10의 보수는 6이고, 10진수 2의 10의 보수는 8이다.
보수는 컴퓨터에서 음의 정수를 표현하기 위해서 고안.
컴퓨터 내부에서는 사칙연산을 할 때 덧셈을 담당하는 가산기(Adder)만 이용하기 때문에 뺄셈은 덧셈으로 형식을 변환하여 계산해야 한다.
즉 컴퓨터 내부에서는 A - B를 계산할 때 B의 보수(-B)를 구한 다음 A + (-B)로 계산하는 것이다.

▶ 1의 보수 : 각 자릿수의 값이 모두 1인 수에서 주어진 2진수를 빼면 1의 보수를 얻는다.
​
  Ex) 2진수 1010의 1의 보수는 0101.
​
▶ 2의 보수 : 1의 보수에 1을 더한 값과 같다.​
​
  Ex) 2진수 1010에 대한 2의 보수를 구하려면 2진수 1010에 대한 1의 보수 0101을 구한 다음 1을 더해 0110을 얻는다.
```

즉, 2의 보수법을 적용하려면 1의 보수법을 거쳐야 한다.

첫째, 128을 이진수로 변환하면 => 10000000

둘째, 1의 보수법을 거치면 => 01111111

셋째, 1의 보수 01111111에 +1을 한다. 결과는 10000000

<br>
난 똥멍청이라 맨 처음에 +1을 더한 저 결과를 바로 이해 못했다.

<img width="70%" alt="스크린샷 2021-10-29 오후 5 27 31" src="https://user-images.githubusercontent.com/76654131/139402353-1e76aa43-97b6-4a16-bb88-ae3f4f5a5fcf.png">

- **Signed** : 제일 앞 비트인 MSB를 하나 소비  
  <img width="70%" alt="스크린샷 2021-10-29 오후 5 49 06" src="https://user-images.githubusercontent.com/76654131/139405698-c4a5324b-8cbb-4496-815a-bae6974b5895.png">
  <br>

---

## 이렇게 Signed 와 UnSigned는 메모리 저장 방식이 다르다.

그래서 Signed에서 11111111이 십진수로 -1이지만 UnSigned에서는 십진수로 255가 되는 경우가 있는것이다.

이래서 간혹 Signed와 UnSigned를 서로 연산할 때, Signed를 UnSigned쪽으로 바꿔서 연산하면<br>
Signed의 음수부분이 바껴서 버그가 발생하기도 한단다.

<br>
흠... 그럼 어떤걸 사용하는게 좋은거지?

<br>
근데 Signed가 **<font color="red">음수</font>**일때 UnSigned으로 바꾸는 경우에만  메모리 저장 방식이 달라 값이 달라지는거지,   
Signed가 **<font color="#1E90FF">양수</font>**이면 UnSigned로 동일한 값으로 잘 바뀐다.
 
<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://m.blog.naver.com/kmc7468/220792205439](https://m.blog.naver.com/kmc7468/220792205439)  
> [https://themangs.tistory.com/entry/Signed와-Unsigned의-차이](https://themangs.tistory.com/entry/Signed와-Unsigned의-차이)  
> [https://ndb796.tistory.com/4](https://ndb796.tistory.com/4)
