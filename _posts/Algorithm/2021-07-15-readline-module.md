---
layout: post
title: "[백준/Node.js] readline 모듈 입출력 방법"
category: Algorithm
tags: [algorithm, baekjoon, node.js 입출력]
comments: true
---
<br>
<br>
백준 1단계를 fs 모듈로 풀었고, 2단계 if문 문제를 readline 모듈로 풀어보기 위해
readline 모듈을 이용한 입출력 방법을 알아볼거다.

---

## readline 모듈

- 입출력을 다루는 built-in 모듈인 readline을 이용해서 사용자가 입력한 콘솔 입력 값을 한 줄 단위로 읽어오는 역할을 한다.
- 한번에 한줄씩 readable 스트림(Ex.process.stdin)에서 데이터를 읽어오는 모듈이다.

>**스트림** :  운영체제에서 파일이나 프로세스에 접근할 때 사용하는 소프트웨어적인 상태
               컴퓨터 프로그램과 그 환경(일반적으로 단말기) 사이에 미리 연결된 입출력 통로

*보통 입출력은 물리적으로 연결된 키보드와 모니터를 통해 일어나는데 표준 스트림은 이와 같은 과정을 추상화한 것*

```javascript
//Node.js의 built-in module인 readline 모듈을 가져온다.
const readline = require('readline');
 
//createInterface 메소드를 사용하여 인터페이스를 생성한다.
//input에서는 사용자의 입력을 받기 위해 process.stdin을 사용하고
//output에서는 출력 이벤트를 위해 process.stdout을 사용했다. 
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
 
// 앞으로 구현할 프로그램의 실행컨텍스트에 input이라는 변수를 선언했다.
// 아래의 line 이벤트에서 처리할 입력들이 이 곳에 들어오게 될 것이다.
let input = [];
 
// line 이벤트가 발생할 시의 로직을 실행하는 이벤트이미터를 정의한다.
// 파일을 읽어들이는 중에 줄바꿈문자 /n을 감지하면 'line'이벤트가 일어난다.
// 이 때 읽어들인 내용인 line을 매개변수로 넣어서 콜백에서 처리를 하면된다.
rl.on('line', function (line) {
  
  // 위에서 선언한 input에다가 읽어들인 내용 중 한 줄인 line을 처리하자.
  // 백준에서 입력값은 공백을 기준으로 구분되니 split(' ')을 이용하여 array로 만든 후
  // 이하의 연산에서 정수로 활용되어야 하니 .map((el) => parseInt(el))를 이용하여
  // 모두 정수로 만들어주자.
  input = line.split(' ').map((el) => parseInt(el));
}).on('close', function () {
  
  // 아래부터 실제 구현부이다. 문제를 풀 때에는 여기에다가 로직을 구현하면 된다.
  // 아래는 백준 1008번 문제이다.
  let num1 = Number(input[0]);
  let num2 = Number(input[1]);
    
  console.log(num1/num2)
  // 프로세스의 실행을 종료하고 프로그램을 끝낸다.
  process.exit();
});

```
이 코드를  콘솔에서 실행하면 **'close' 이벤트**에 걸리지 않아서  console.log가 찍히지 않고 입력만 계속 받는다.   
이유는 잘 모르겠지만, 콘솔 interactive shell 이라는것 때문에 자동으로로 close가 호출되지 않는다고 한다.
 
이 경우, 아래 그림과 같이 **rl.close() 메소드**를 호출하면 **'close'이벤트**가 발생되어 한 줄 입력 받기로 넘어가 console.log가 출력된다.


```javascript
rl.on('line', function(line) {
     input = line.split(' ').amp((el) => parseInt(el));
    rl.close();
}).on('close', function() {
```

### 코드보고 이해가 잘안가는 부분은 밑에 자세하게 설명해놨으니 보면 이해가 갈것이다.

---

## rl.close()

rl.close()메소드는 readline.interface인스턴스와 입력 및 출력 스트림 제어를 종료한다.   
rl.close()메소드가 호출되면 readline.interface 인스턴스에서 'close 이벤트'가 발생된다. 

## rl.on()

readline.Interface 인스턴스(rl)에서 .on()메소드로 Interface가 내장한 이벤트들을 실행한다.   
생성된 readline.Interface 인스턴스에서 가장 많이 쓰이는 이벤트는 'line'이벤트다.

## Event : 'line'

'line'이벤트는 입력(input) 스트림이 줄바꿈(end-of-line) 입력(\n, \r or \r\n)을 받을  때마다 발생한다.   
<u>쉽게 말해 일반적인 사용자가  <Enter> or <Return> 키를 누를 때 발생한다는 소리다.
* 콜백 함수는 한 줄의 수신 된 입력내용을 문자열타입의 파라미터로 받으며 호출된다.

```javascript
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
 
rl.on('line', function(line) {
  // line을 가공하여 변수에 저장
  
}).on('close', function() {
  // 저장된 변수를 이용하여 계산 후 출력
});
```

## Event : 'close'

< **'close'이벤트**가 발생하는 상황 >
- rl.close() 함수가 호출되어 readline.Interface 인스턴스가 입출력 스트림의 권한을 포기한 상태일 때
- 입력 스트림이 'end'이벤트를 받은 경우
- 입력 스트림이 Ctrl + C / Crtl + D 를 받은 경우.    <mark style='background-color: #ffdce0'> // 여러줄 입력 받을 때 close하는 법 </mark>

정리하자면,
<mark style='background-color: #dcffe4'> readline 모듈 </mark>을 사용할 경우 각 줄이 입력될 때마다 <mark style='background-color: #fff5b1'>'line' 이벤트</mark>가 매번 발생하여 이를 변수에 저장하며,
<mark style='background-color: #ffdce0'>'close' 이벤트</mark>가 발생한 경우 저장된 변수를 가지고 계산을 진행하는 것이다.
 
만약 여러줄을 입력 받아야 한다면, 아래와 같이 하면 된다.

```javascript
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
 
let input = [];
 
rl.on('line', function (line) {
    input.push(line);
  })
  .on('close', function () {
    console.log(input);
    process.exit();
});
```
이 경우도 위에서 말했던것처럼 콘솔에서 **'close' 이벤트**가 걸리지 않기 때문에 
콘솔에서 **Ctrl + C / Crtl + D**를 입력해서 **'close' 이벤트**를 발생시켜야 한다.

## String.prototype.split()
- 문자열을 일정한 구분자로 잘라서 배열로 저장   

>**split() : 구분자가 없기 때문에 문자열 그대로 리턴**     
**split('') : 공란문자 즉 글자 하나하나로 구분된다.**      
**split(' ') : space 문자를 기준으로 구분된다.**

---

## 결론 
fs모듈보다 입력량이 상당히 많아 복잡한 문제는 힘들것 같다...
 
코딩테스트에서는  입력을 받은 뒤에 계산을 하고 출력을 한다고 한다.
계산 도중에 인터랙티브하게 유저로부터 입력을 받는 일이 없기 때문에  이벤트 드리븐 방식?의 복잡한 readline 모듈을
사용할 필요가 전혀 없다. 항상 fs.readFileSync(0, "utf8")을 사용하는걸 추천한다고 한다.
 
그런데 현재 내 상황에서는 알고리즘을 푸는데 있어 이러한 모듈을 아는것보단, 문제 해결 능력을 키우는게 우선이기에
모듈 상관없이 닥치고 많은 문제를 풀어보는게 답인것 같다.

<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://velog.io/@grinding_hannah/JavaScript-Node.js에서-readline-입력받기](https://velog.io/@grinding_hannah/JavaScript-Node.js에서-readline-입력받기)   
[https://velog.io/@bigsaigon333/Javascript로-코딩테스트-준비하기1-입출력](https://velog.io/@bigsaigon333/Javascript로-코딩테스트-준비하기1-입출력)   
[https://velog.io/@two_jay/Node.js로-백준-문제를-풀어보자](https://velog.io/@two_jay/Node.js로-백준-문제를-풀어보자)