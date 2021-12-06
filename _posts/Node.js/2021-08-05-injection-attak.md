---
layout: post
title: Injection Attak
category: Node.js
tags: [node.js]
comments: true
---
<br>
데이터 값을 가져오는 방식으로는  **`body`** 랑 **`query`**가 있다. 

### ✓ &nbsp;body data : req.body

-- Client에서 보내주는 JSON, XML, Multi Form 등의 데이터를 담는다. 주소에서는 확인할 수 없다.

### ✓ &nbsp;주소 (query string) : req.query

-- 주소 바깥 ? 이후의  변수를 담는다. ? 뒤에 오는 것들이 바로 query string

- **req.query**는 순수 node.js에는 없는 명령어다. **Express** 환경에서 주어지는 명령어다.

- **req.query** 문을 통해 데이터를 가져오면 client가 url을 통해 요청한 데이터를 내보낼 수 있다. 

#### 호출 : localhost:3000?idx=1&name=asdf   \=>  req.query가  { idx: '1', name: 'asdf' } 처럼 객체 형태로 값을 받아온다.

---

## Injection Attak

그럼 본격적으로  **`Injection Attak`** 에 대해 알아보자.

아래와 같이 **쿼리폼**을 활용해 sql이라는 쿼리문을 만들었다. 

```
let sql = 'SELECT * FROM products WHERE idx = "'+idx+'"'
```
<br>
우리가 예상하는 모습은 다음과 같다.

#### 호출 : **localhost:3000?idx=1**

#### 적용 된 sql : **SELECT \* FROM products WHERE idx = "1"**

=> idx = 1 에 해당하는 데이터를 가져오게 됨

<br>
하지만 이러한 **쿼리폼**은 **Injection Attak(인젝션 공격)** 에 **<font color="red">취약한</font>** 형태이다.
<br>
### ❗️ 인젝션 공격 

호출(<font color="red">공격</font>) : **localhost:3000?idx=whatever" or 1="1** 

적용 된 sql : **SELECT \* FROM products WHERE idx = "whatever" or 1="1"**

**<font color="red">=> 모든 데이터를 가져오게 됨</font>** 

---

## Injection Attak을 막는 방법

#### 인젝션 공격을 막는 방법
**1. escape 함수(변수를 string으로 encoding 해주는 함수)**

**2. Bind 변수(=?) 활용, 3. 쿼리안에 timeout 을 거는 방법 등이 있다.**

### `바인딩 쿼리`

**그 중 가장 간편하고 권장되는 방식 Bind 변수(=?)를 활용해 아래와 같이 쿼리문을 작성해보자.**

```javascript
 //권장되는 방식

 // const product = req.body
 
 // INSERT
 pool.query('INSERT INTO products SET ?',
 	product, 
    function (error, results, fields) {
    if (error) throw error;
    // Neat!
 });


// SELECT
 let columns = ['name'] // 1개일때는 array 아니어도 됨
 pool.query('SELECT ?? FROM ?? WHERE idx = ?', 
   [columns, 'products', idx], 
   function (error, results, fields) {
   if (error) {
     console.log('error : ', error)
   };
   // ...
   res.json({results})
 });
```

#### 변수가 삽입될 부분을 'Bind 변수'라고 불리는 "?"로 대체하여 쿼리문을 작성한다.
#### 그리고 **`INSERT문`**을 보면 SET 다음 ? 에 Client가 입력한 정보인 product가 할당되는 것이다.

<br>
참고로 Client가 입력한 정보인 product가 테이블 products의 column들에 포함되어 있다면 일일이 적어줄 필요가 없다.

DB에 이미 테이블 products의 column들이 할당되어 있기 때문에

Client가 입력한 정보인 product가 column에 맞게 알아서 찾아  들어가준다.

**_<u>어차피 프론트에선 정해진 규칙대로 정보를 보내야 하기 때문이다.</u>_**

이때 Bind 변수는 자체적으로 들어오는 데이터를 필터링하고 위험한 요소를 제거해준다.

따라서 정상적이지 않은 방식으로 접근했을 때 결과값을 출력하지 않는다.

#### `SELECT문` 을 통해 알아야 할 것

-   Bind 변수에서는 물음표 2개(??)는 table, columns 등이 필요할 때 사용되고 물음표 1개(?)는 실제 값을 넣을 때 사용한다.
-   배열변수에 ? 가 할당된 순서대로  변수를 할당한다.


<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://jungeunpyun.tistory.com/21?category=911250](https://jungeunpyun.tistory.com/21?category=911250)