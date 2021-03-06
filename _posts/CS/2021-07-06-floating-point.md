---
layout: post
title: 부동소수점
category: CS
tags: [cs, computer architecture]
comments: true
---

#### _<center>" 어릴때 태권도를 하면서 수없이 들어온 부동자세,<br>움직이지 말아야 할 것 같은 단어 <font color='red'>'부동'</font>이다.<br>하지만 부동소수점은 영어로 <font color='#1E90FF'>floating point</font> = '소수점(point) + 둥둥 떠다닌다(floating)'<br>쉽게 말해 소수점이 움직인다는 의미다. "</center>_

---

사람은 수를 표현할 때 기본적으로 10진법을 사용하지만, 컴퓨터는 0,1만 쓰는 2진법으로 저장한다.  
학창시절 10진수, 2진수 접해본 기억이 있을거다.

10진수에서는 10^n에 해당하는 수가 될 때마다 자릿수가 올라갔다면, 2진수에서는 2^n에 해당하는 수가 될 때마다 자릿수가 올라간다. ex) 10진수 4를 2진수로 100, 8은 1000

<p align="center"><img width="30%" src="https://user-images.githubusercontent.com/76654131/138600157-d80e72fa-c90b-4d1d-8b10-aa12c077681a.png"></p>

정수는 이렇게 쉽지만, 컴퓨터에서 소수점이 붙어있는 실수를 2진수로 표현하는 것은 복잡하다.

---

### 고정 소수점(fixed point) 방식

10진수를 2진수로 바꾼 뒤 소수부의 자릿수를 미리 정해, 고정된 자릿수의 소수를 표현하는 가장 간단한 방식
쉽게말하면 2진수로 변환한것을 그대로 집어 넣는 것이다.

ex) 7.625 => 111.101

<p align='center'><img width="50%" src="https://user-images.githubusercontent.com/76654131/138600250-0ee335e9-4a5f-43a6-a921-3b07e28cda73.png"></p>

---

## 부동 소수점(floating point) 방식

고정 소수점과 달리 2진수로 변환한 결과를 정규화 과정 등을 통해 지수부와 가수부에 나누어 표현한다.

- 정규화 (Normalization

정규화라는 단어는 수학이나 컴퓨터 분야에서 다양한 의미로 쓰이지만 여기서 말하는 정규화라는 것은 2진수를  
1.xxxx... \* 2^n 꼴로 변환하는 것을 말한다.

우리는 부동소수점 방식으로 실수를 저장하는 과정에서 <u>floating point의 어원</u>을 이해할 수 있다.

ex) 7.625 => 111.101을 정규화(1.xxxx... _ 2^n) 하려면 정수부에 1만 남을 때까지 소수점을 왼쪽으로 이동시켜야 한다.  
 여기서 <u>소수점이 이동</u>한 칸 수 만큼 n 자리에 적용하면 1.11101 _ 2^2

<p align='center'><img width="80%"  src="https://user-images.githubusercontent.com/76654131/138600361-efbb7f40-8d9b-422e-8d54-09ff20abf2c7.png"></p>

정규화 결과(1.11101 \* 2^2)를 토대로 소수점 오른쪽에 있는 숫자들이 그대로 11101이 가수부에 들어가면 되고  
지수부에는 2^n = 2^2 에서 n에 해당하는 지수 2를 2진수로 변환해 들어가면 된다.

하지만 여기서 중요한것이 IEE 표준에 의하면 지수를 그대로 변환해 넣으면 안되고 비트마다 정해진 <font color='#1E90FF'>bias</font>라는 숫자를  
더한 다음 변환해서 넣어야 한다.

말이 좀 복잡한데 예를 들어 위에 그림처럼 32비트를 쓰는 경우 IEEE표준 <font color='#1E90FF'>bias</font>가 127이다.  
그러므로 2 + 127 = 129 => 2진수로 변환한 숫자가 지수부에 들어가게 되는 것이다.

왜 굳이 이렇게 bias라는 값을 쓰면서 복잡하게 하나 했는데, 지수가 음수가 되는 경우가 있을 수도 있기 때문이다.  
ex) 0.000101 를 정규화 하면 1.01 \* 2^-4  
이런 경우 지수 -4를 지수부에서 음수부분을 어떻게 표현할수가 없기 때문에 <font color='#1E90FF'>bias</font>가 필요한것이다.

#### -- 부호 비트는 지수의 부호를 뜻하는게 아니라 전체 숫자의 부호를 뜻하는 거라서 상관이 없다.

<br>
 
프로그래밍을 처음 접해본 언어가 JAVA였는데 실수형 타입을 배울때 float, double이 있었다.   
나는 둘다 그냥 실수를 표현주는 타입으로 생각하고 double만 주로 썼었다.
 
알고보니 32비트 체계를 32비트 단정도 (Single-Precision) 라고 부름 => 여기서 <mark style='background-color: #ffdce0'>float</mark>   
64비트 체계를 64비트 배정도 (Double-Precision)  라고 부름 => 여기서 <mark style='background-color: #dcffe4'>double</mark>
 
 
float는 부동소수점 방식을 사용하는 기본형이라는 의미로 <mark style='background-color: #ffdce0'>float</mark>ing point에서 따왔고,  
double은 64비트 배정도를 사용한다는 의미로 <mark style='background-color: #dcffe4'>double</mark>-precision에서 나온 것이다.

<p align='center'><img width="60%" src="https://user-images.githubusercontent.com/76654131/138600515-dbb6d945-5c5d-4d42-b288-fe0cb435f9e8.png"></p>

- 64비트에서 지수부가 11비트 = 2^11 즉 2048개의 수를 표현할 수 있으므로 0~1023 구간은 음수,  
  1024~2047 구간은 양수 지수를 의미하며 bias는 1023이 된다.

---

## 고정소수점 vs 부동소수점

위에서 알아본 고정 소수점 방식은 고정된 자릿수로 인해 제한적이어서 표현할 수 있는 범위가 매우 작다.  
하지만 부동 소수점 방식은 표현 가능한 수의 범위와 정밀도에서 우위가 있기 때문에 매우 큰 실수까지도 표현할 수 있다.

그래서 고정소수점 방식은 거의 안쓰이고 높은 정밀도를 요구하는 현재 컴퓨터 시스템에서는 대부분 **<font color='#1E90FF'>부동 소수점 방식</font>**을 사용한다.

**<font color="red">하지만 부동소수점 방식에도 오차가 있을 수 있다.</font>**

부동소수점 방식을 사용하면 표현할수 있는 범위는 매우 크지만 10진수를 정확하게 표현하는것은 힘들다.  
컴퓨터가 실수를 표현하는 것은 언제나 **<font color='#1E90FF'>근사치</font>**를 표현하기 떄문이다.

<p align="center">
<img width="60%" src="https://user-images.githubusercontent.com/76654131/138600792-c2b56d57-0d2c-4bee-acbb-04e2f4480537.png"></p>

---

#### _<center>" 컴퓨터에서 실수를 가지고 수행하는 모든 연산에는 언제나 작은 오차가 존재한다.<br>그래서 알파고가 이세돌한테 졌나보다. "</center>_

<br>
<br>
<br>
   
>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://gsmesie692.tistory.com/94](https://gsmesie692.tistory.com/94)   
[https://tcpschool.com/cpp/cpp_datatype_floatingPointNumber](https://tcpschool.com/cpp/cpp_datatype_floatingPointNumber)
