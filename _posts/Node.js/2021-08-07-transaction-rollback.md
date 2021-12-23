---
layout: post
title: Transaction과 Rollback
category: Node.js
tags: [node.js]
comments: true
---
#### <center>" 데이터 베이스를 <font color="#0086E5">수정</font>하는 것은 상당한 <font color="red">리스크</font>가 있는 일이다.<br>때문에 데이터를 수정할 때는 실제로 DB에 적용하지 않고 취소하는 기능이 필요하다.<br>이렇게 데이터를 실제로 수정하지 않고 취소 처리하는 것을 " Rollback "이라고 하며,<br>" Rollback "하기 위해서는 " Transaction "을 통해 쿼리 명령어를 실행해야 한다. "</center> 
<br>
<br>
이번 포스팅에선 SQL 절들을 수행 할 때, 모두 수행 되지 않을 경우, 원래의 상태로 돌리는 트랙잭션 처리에 대해서 알아보자.

---

## Transaction (트랜잭션)

- 연속된 작업을 뜻하는데, DB에서 이러한 트랙잭션은 DB 상태를 변화시키는 "**쪼개질 수 없는 작업 단위**"를 뜻한다.

▶ **ATM으로 계좌이체를 한다고 생각해보면,**

1. A 은행에서 출금하여 B은행으로 송금하려고 한다.

2\. 송금 중, 알 수 없는 오류가 발생하여 A은행 계좌에서 돈은 빠져 나갔지만 B은행의 계좌에 입금되지 않았다.

3\. 이와 같은 상황을 막기위해 거래가 성공적으로 모두 끝나야 이를 완전한 거래로 승인하고, 거래 도중 뭔가 오류가 발생했을 때는 이 거래를 처음부터 없었던 거래로 완전히 되돌린다.

이렇게 거래의 안정성을 확복하는 방법이 **`트랜잭션 처리`**이다.

---

## 트랙잭션 처리

-   트랜잭션을 모두 **<font color="#0086E5">성공</font>**/**<font color="red">실패</font>**를 하기 위한 처리이다.
-   **<font color="#0086E5">성공</font>**에 대해서는 신경쓸께 없지만, **<font color="red">실패</font>**일 경우, 작업중에 건들였던 테이블들을 모두 작업전으로 돌리는 작업이 필요하다.  
    **즉, 되돌리는 작업을 트랜잭션 처리라고 한다**.  
    <u>DB에선 처리 과정이 모두 성공했을 때만 최종적으로 DB에 반영합니다.<u>

<br>
내 계좌의 잔액에서 이체한 금액만큼 빼는 일과, 상대 계좌의 잔액에서 해당 금액만큼 더하는 일은 쪼개어져서는 안된다.    
두가지 명령 중 하나만 실행되서는 안되며 하나의 작업으로 함께 진행되어야 하는 일이기 때문이다.

#### <u>즉, 더이상 쪼갤 수 없기 때문에 일부만 동작해선 안된다는 것이 트랜잭션의 핵심이다.</u>

#### 부분 작업들 여러개가 모여진 이러한 트랜잭션을 처리하기 위해 DB는 다음의 두가지 명령어를 활용하는데,
#### 바로 **`Rollback(롤백)`** 과 **`Commit(커밋)`**이다. 
#### ✓ **rollback**과 **commit**은 Transaction 안에서 동작을 한다.

-   **Rollback(롤백) :**부분 작업이 실패하면 작업을 무효화하고 트랜잭션 실행 전으로 되돌린다.
-   **Commit(커밋) :** 모든 부분작업이 정상적으로 완료하면 이 변경사항을 한꺼번에 DB에 반영한다.  
    

<p align="center"><img width="629" alt="스크린샷 2021-12-24 오전 3 17 38" src="https://user-images.githubusercontent.com/76654131/147278254-fce0dae0-f79d-4bb4-862e-e432c5b18f7f.png"></p>

<br>
#### ❗️ 명령어들을 트랜잭션으로 묶으려면 SQL 서버에선 : BEGIN TRANSACTION ~ COMMIT TRANSACTION

```javascript
// Rollback 예제

router.post('/', function (req, res, next) {
  const body = req.body
  // pool.getConnection으로 connection을 가져옴
  pool.getConnection(function(err, connection) {
      if (err) throw err; // not connected!
      // beginTransaction으로 트랜잭션 처리 시작
      connection.beginTransaction(function(err) {
          if (err) { 
              res.status(200).json({error:err})                
          }            
          connection.query(
              'INSERT INTO products SET ?', 
              body,
              function (error, result, fields) {
                  if (error) {
                      connection.release() // 에러시 connection을 pool에 반납
                      return connection.rollback(function() { // rollback => 무효화                                   
                          res.status(200).json({error:error})                            
                      })
                  } 
                  connection.commit(function(err) { // commit => 쿼리를 실행시켜라
                      connection.release() // committed; 트랜잭션 종료했으니 반납
                      if (err) {
                          return connection.rollback(function() { // rollback => 무효화
                            res.status(200).json({err:err})                                
                          })
                      }
                      res.status(200).json({result})
                  })                       
          })          
      })
  })
})
```

#### ❗️ 트랜잭션 처리는 INSERT, UPDATE, DELETE 문만 가능하며, 다른것들은 트랙잭션 처리 되지 않는다.

> **왜 GET문은 안돼?**  
> Get문은 정보를 가져오기만 하지, DB 상태를 변화시킬 일이 없기 때문에 트랙잰션 처리가 필요가 없고,  
> 수시로 데이터를 받아와야 하므로 DB와의 연결을 유지하고 있어야 하기 때문이다.


<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://www.ikpil.com/1110](https://www.ikpil.com/1110)   
[https://devuna.tistory.com/30](https://devuna.tistory.com/30)