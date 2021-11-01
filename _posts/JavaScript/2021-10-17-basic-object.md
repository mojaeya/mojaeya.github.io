---
layout: post
title: JavaScript - 객체의 기초
category: JavaScript
tags: [javascript, 모던 JS 입문]
comments: true
---

# 1. 객체지향 프로그래밍(Object-oriented programming)이란?

- 객체지향 프로그래밍이란 '객체'라는 개념을 기반으로한 프로그래밍 패러다임중 하나이다.
- 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립된 '객체'들의 모임으로 파악하고자 하는 것이다. 각각의 객체는 메시지를 주고받고, 데이터를 처리할 수 있다.
- 객체지향의 기본 개념은 '실제 세계는 사물(객체)로 이루어져 잇으며, 발생하는 모든 사건들은 사물간의 상호작용'

##  📌  클래스와 객체 그리고 인스턴스의 개념 

### 클래스 ( Class )

- 객체를 만들어 내기 위한 설계도

### 객체 ( Object )

- 소프트웨어 세계에 구현할 대상
- 클래스에 선언된 모양 그대로 생성된 실체
- '클래스의 인스턴스'

### 인스턴스 ( Instance )

- 설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체
- 즉, 객체를 소프트웨어에 실체화 하면 그것을 ‘인스턴스’라고 부른다.
- 실체화된 인스턴스는 메모리에 할당된다.
- 추상적인 개념과 구체적인 객체 사이의 관계 에 초점을 맞출 경우에 사용한다. => ‘ ~의 인스턴스 ’ 의 형태로 사용된다.

>인스턴스라는 용어는 반드시 클래스와 객체 사이의 관계로 한정지어서 사용할 필요는 없다.   
어떤 원본(추상적인 개념)으로부터 ‘생성된 복제본’을 의미한다. 

**[ class 기반의 객체 지향 언어의 객체 생성 방법 ]**
- 클래스 객체변수명 = new 클래스();
- 잘못된 통상적인 예시 : ~~붕어빵틀 붕어빵 = new 붕어빵틀();~~
<p align="center"><img width="70%" src="https://user-images.githubusercontent.com/76654131/136685291-cd7a1773-5324-4784-8716-b25cdc481840.png"></p>   

```java
// JAVA
Public class Main {
  public static void main(String[] args) {
  
  Bell a;  // 객체 : 벨
  a = new Bicycle(); // 인스턴스
  a.name = tacobell
  a.color = yellow  
  a.horn2()

class Bell { // 클래스 : 벨을 만드는 설계도
  String name;
  double color;

  void horn1() {
    System.out.println("띵~");
  }
  void horn2() {
    System.out.println("따르릉~");
  }
}
```
### 객체와 인스턴스 

- 클래스의 타입으로 선언되었을 때 객체라고 부르고, 그 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라고 부른다.
- 객체는 현실 세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다.
- 객체는 ‘실체’, 인스턴스는 ‘관계’에 초점을 맞춘다. 그래서 객체를 ‘클래스의 인스턴스’라고도 부른다.
- 그러므로 어렵다면, 인스턴스는 객체에 포함된다고 봐도 된다.

---

# 2. 자바스크립트는 prototype 기반의 객체 지향 언어이다.
<br>
&nbsp; 자바스크립트 외 객체 지향 언어로는 JAVA, Python, Ruby 등등이 있다. 이러한 객체 지향 언어들은 Class라는 개념이 존재하고 상위 class의 속성을 Instance로 불리는 하위 객체가 내려받을 수 있다.   
&nbsp; 자바스크립트는 prototype 기반이기 때문에 다른 객체 지향 언어들과 달리 Class와 그에 따른 Insatance 개념이 존재하지 않는다. 대신, 자바스크립트는 생성자 함수와 new 키워드를 이용해 Class와 Instance 개념을 구현할 수<U>(흉내낼 수)</u> 있다.   
&nbsp; 참고로 자바스크립트는 ES6 버전에서 Class라는 문법을 추가하였지만, 언어 기반 자체가 바뀐 것은 아니다.

```javascript
// ES6 버전에서 Class 문법을 추가되기 전 자바스크립트
function Bell(name, color) {  // 객체를 생성하는 함수 : 생성자 함수
    this.name = name        // 여기서 this는 생성자 함수 자신을 가리킨다.
    this.color = color
    this.horn2 = function() { // 프로퍼티에 저장된 값이 함수면 그 프로퍼티를 메서드라고 한다.
        console.log("따르릉")
    }
}

const a = new Bell('tacobell', 'yellow')

a.name
a.color
a.horn2()


// 프로토타입 => 유전자라고 생각하자
function Bell(name, color) {
    this.name = name
    this.color = color
}
Bell.prototype.horn2 = function() {
   console.log("따르릉")
}

const a = new Bell('tacobell', 'yellow')

a.horn2()


// class 문법 추가
class Bell {
    constructor(name, color) {
        this.name = name
        this.color = yellow
    }

    horn2() {
        console.log("따르릉")
    }
}

const a = new Bell('tacobell', 'yellow')
a.horn2()
```
---

# 3. 객체의기초 (객체 리터럴)

<p align=center><img width="30%" src="https://user-images.githubusercontent.com/76654131/136683293-43725012-fad2-406e-a761-587d450ce5ca.png"></p>

### 🔎 <font color='black'> 서랍장을 객체라고 생각해보자 </font>

- 서랍장 안에 있는 파일 : 프로퍼티

- 파일에 각각 붙어있는 이름표 : 프로퍼티 이름 또는 키

- 객체에선 키를 이용해 프로퍼티를 쉽게 찾을 수 있다.


<p align="center"><img width="30%" src="https://user-images.githubusercontent.com/76654131/136693990-67205048-dadc-4232-a6e7-dbc975f99405.png"></p>

```javascript
let card = new Object(); // '객체 생성자' 문법
let card = {};  // '객체 리터럴' 문법

let card = { suit: "하트", rank: "A" }
```
👋 중괄호 안에는 ‘키(key): 값(value)’ 쌍으로 구성된 프로퍼티(property) 를 여러 개 넣을 수 있는데, 키엔 문자형, 값엔 모든 자료형이 허용된다.

## 📌 객체는 참조 타입 

- 생성된 객체는 메모리를 차지하는 한 덩어리가 된다. 객체 타입의 값을 변수에 대입하면 그 변수는 그 객체를 참조하게 되는것이다.
- 아래 그림과 같이 변수 a가 card 객체를 참조하게 되므로 a로 card 객체를 읽거나 수정 가능

<p align="center"><img width="90%%" src="https://user-images.githubusercontent.com/76654131/136694954-1ffd414b-f968-454b-9b4e-a5815f073b09.png"></p>

<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://cloudstudying.kr/lectures/373](https://cloudstudying.kr/lectures/373)   
[https://ko.javascript.info/object](https://ko.javascript.info/object)
