---
layout: post
title: 변수와 값
category: JavaScript
tags: [javascript, 모던 JS 입문]
comments: true
---
## 변수 
    - 값(데이터)을 담기 위해 이름 붙인 상자
    - 변수는 어떤 정보에 이름을 붙여서 저장하고 싶을 때 사용함. 이때, 컴퓨터 메모리 공간에 일정한 크기로 생성됨
    
    const myNumber = 23

![image](https://user-images.githubusercontent.com/89966610/136694701-b1ee32e8-ec17-49a4-a383-0decb912fb42.png)

## 변수 선언
    - 선언자를 사용하여 변수 이름을 선언
    - 선언자 종류: var, let, const
    
    const name = "Lily"
    

   구분 | 재선언 | 재할당 | 참고 |
   ----- | ----- | ----- | -----
   var | O | O | | 
   let | X | O | let 재할당: let을 제외하고 작성 let name = "Lily"  /..../ name = "Jane"|
   const | X | X | 절대로 바뀌지 않는 상수(파이, 생일, 최댓값 등)를 선언할 때 사용 |


    *TIP: 모든 변수를 const로 선언하고 나중에 변경될 여지가 있는 변수들만 let으로 바꾸면됨
    
    *참고

    = (대입 연산자) : 오른쪽 값을 왼쪽 변수에 대입한다는 뜻

    == (일치 연산자) : 5 == '5' //true
                      
                       5 == 5 //true

    === (동등 연산자) :  5 === '5' //false
             
                         5 === 5 //true


## 변수 선언 생략
     - var문으로 선언하지 않은 변수 값을 읽으려고 시도하면 참조 오류 발생
     
      console.log(x); // ReferenceError : x is not defined
     
     - var문으로 선언하지 않은 변수에 값을 대입할 때는 오류가 발생하지 않음 
     
        x = 2;
        console.log(x); // 2 
 
 
    변수를 선언하지 않은 상태에서 값을 대입하면 자바스크립트 엔진이 그 변수를 자동으로 전역 변수로 선언하기 때문.
    그러나 변수를 선언하지 않고 변수를 사용하는 행위는 버그의 원인 될 수 있음.
    따라서 변수는 반드시 선언하고 사용해야 한다.

## 변수 끌어올림(호이스팅, hoisting)
    - 프로그램은 작성한 순서에 따라 윗줄부터 차례대로 실행됨 but 변수 선언은 이 원칙을 따르지 않음
    - 변수 선언의 끌어올림은 다른 언어에는 없는 자바스크립트만의 고유한 특징

    console.log(x); // → undefined

    var x;


    console.log(x); // → undefined

    var x = 5;

    console.log(x); // → 5


## 변수의 명명 규칙
    1. 사용 가능 문자: 유니코드 문자, 숫자(0~9), 밑줄(_), 달러 기호($)
      * 문자 중 기본적으로 영어단어 사용
      
    2. 첫 글자에 숫자 사용 X  // const 1st = "1"
    
    3. 예약어를 변수로 사용 X  // const const = "1"
    
    4. 가급적 상수는 대문자로 사용  // const MAX-SIZE = "1"
    
    5. 변수가 어떤 정보를 가지고 있는지 유추하기 쉽도록  // const age = "20"
    

    + 루프 카운터 변수(7장) 이름으로는 i,j,k 등을 사용
    + 논리값(3.2.5절)을 표현하는 변수에는 이름 앞에 is를 붙임 isMouseDown
    + 생성자(4.3절) 이름을 붙일 때는 파스칼 표기법을 사용
    
    
    식별자 명명 규칙에 따라 자유롭게 지정 가능 but 협업 및 원활한 프로그래밍을 위해,
    일정한 표기법(일반적으로 세가지)에 따라 변수의 의미를 알 수 있도록 설정할 것
   - 캐멀 표기법(로어 캐멀 표기법)
    
           두 번째 이후 단어의 첫 글자를 대문자로 표기하고 나머지는 소문자로 표기

           Ex) newName createLifeGame
   
   - 파스칼 표기법(어퍼 캐멀 표기법)
   
           각 단어의 첫 글자를 대문자로 표기하고 나머지는 소문자로 표기

           Ex) NewName  CreateLifeGame

   - 밑줄 표기법(스네이크 표기법)
   
           모든 단어를 소문자로 표기하고 단어와 단어를 밑줄(_)로 구분

           Ex) new_name  create_life_game
           
           
## 예약어
    - 자바스크립트 문법을 규정짓기 위해 자바스크립트 언어 사양에서 사용하는 특수한 키워드
   
   - ECMAScript 6 기준
   
   break | case | catch | class | const | continue |
   ----- | ----- | ----- | ----- | ----- | ----- |
   dubugger | default | delete | do | else | export |
   extends | false | finally | for | function | if |
   import| in | instanceof | new | null | return |
   super | switch | this | throw | true | try |
   typeof | var | void | while | with | yield |
   
  - 현재는 예약어가 아니지만 ECMAScript 6 이후에 추가될 예정 

   await | enum | implements | package | 
   ----- | ----- | ----- | ----- | 
   protected | interface | private | public | 

  - 미리 정의된 전역 함수

   arguments | Array | Boolean | Date | 
   ----- | ----- | ----- | ----- | 
   decodeURI | decodeURIComponent | encodeURI | encodeURIComponent | 
   Error | eval | EvalError | Function |
   Infinity | inFinite | isNaN | JSON |
   Math | NaN | Number | Object |
   parseFloat | parseInt | RangeError | RefferenceError |
   RegExp | String | SyntaxError | TypeError |
   undefined | URIError | | |

- 위 이름을 사용해도 오류는 발생하지 않음 but 자바스크립트가 가진 본래 기능을 사용할 수 없음

## 데이터 타입과 변수의 동적 타이핑
    - 데이터 타입 : 변수에 저장하는 데이터 종류(ex. 숫자, 문자열 등)
    - 정적 타입 언어 : 변수에 타입이 있는 언어 / 변수의 타입과 일치하는 데이터만 저장 가능
    - 동적 타입 언어 : 변수에 저장된 데이터 타입을 동적으로 바꿀 수 있는 언어
      * 자바스크립트는 변수에 모든 타입의 데이터 저장 가능(변수에 타입이 없기 때문에)
      * So, 자바스크립트는 변수의 데이터 타입에 주의!! 타입 변환에 주의!!
      
## 데이터 타입의 분류
    [자바스크립트 처리 가능 데이터 타입]
    - 원시 타입 : 숫자, 문자열, 논리값, 특수값(undefined, null), 심벌(Symbol)
    - 데이터를 구성하는 가장 기본적인 요소로 불변 값(값을 바꿀 수 업슨 데이터)으로 정의
    - 원시 타입의 값을 원시 값이라 한다. 원시 값을 변수에 대입하면 변수에 그 값이 저장됨
    
    - 객체 타입 : 변수 여러 개가 모여서 만들어진 복합 데이터 타입
    - 원시 타입에 속하지 않는 자바스크립트의 값
    - 객체 안에 저장된 값은 변경 가능
    - 객체는 참조 타입 so, 객체 타입의 값을 변수에 대입하면 변수에는 그 객체에 대한 참조(메모리에서의 위치 정보)가 할당됨
    
## 숫자
    - 자바스크립트에서 숫자는 64비트 부동소수점으로 표현
    - 리터럴 : 프로그램에 직접 작성할 수 있는 상수 값
    
## 문자열
    - 자바스크립트 문자열 : 유니코드 문자(UTF-16 코드)
    - 문자열 리터럴 : "큰따옴표", '작은따옴표?', "큰따옴표 안에 '작은따옴표'", ""
    * 자바스크립트를 HTML 요소에 끼워 넣을 때는 자바스크립트 프로그램을 문자열로 생각!!!
    
    - 이스케이프 시퀀스
    (표 넣기)
    
## 논리값 
    - 논리값 : 조건식이 참인지 거짓인지 표현하기 위해 사용하는 값
    - 논리값 종류: true(참), false(거짓)
    * 자바스크립트에서는 주로 제어 구문(if/else 문, while 문, do/while 문, for 문)에 사용
    
## 특수한 값

 * 값이 없음을 표현하는 특수한 값

   구분  | null | undefined | 
   ----- | -----| -----    |
   의미 | 아무것도 없음 | 정의되지 않은 상태 | 

        [null]
         - 주로 프로그램이 무언가를 검색했지만 찾지 못했을 때 아무것도 없음을 전달하기 위한 값

         [undefined]
                 - 값을 아직 할당하지 않은 변수의 값
                 - 없는 객체의 프로퍼티를 읽으려고 시도했을 때의 값
                 - 없는 배열의 요소를 읽으려고 시도했을 때의 값
                 - 아무것도 반환하지 않는 함수가 반환하는 값
                 - 함수를 호추랬을 때 전달받지 못한 인수의 값
                * 코드로 undefined를 대입한 것이 아니라 자바스크립트 엔진이 변수를 undefined로 초기화 한것!!!

## ECMAScript 6부터 추가된 데이터 타입
     *심벌
        - 자기 자신을 제외한 그 어떤 값과도 다른 유일무이한 값
        
        var NONE = Symbol("none");
        
        var BLACK = Symbol("black");
        
        var WHITE = Symbol("white");
        
        
     *템플릿 리터럴
        - 일부만 변경해서 반복하거나 재사용할 수 있는 틀
        - 역따옴표(`)로 묶은 문자열
        - 일반적인 줄 바꿈 문자 사용 가능
    

<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://github.com/mojaeya/js-study-sunday/blob/main/1.%20Study/1주차/jaewon.md](https://github.com/mojaeya/js-study-sunday/blob/main/1.%20Study/1주차/jaewon.md)