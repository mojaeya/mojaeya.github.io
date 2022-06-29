---
layout: post
title: "MySQL 8.0 | Error: ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client | 오류 해결"
category: MySQL
tags: [mysql, mysql error]
comments: true
---

> MySQL 8.0.25 / Mac OS

`Node.js`에서 `mysql`을 사용하는데 `user`를 `'root'`가 아닌 공부용 DB 스키마 `'dev'`로 설정하고 클라이언트 프로그램에서 사용하려고 했더니 아래와 같은 <font color='red'>오류</font>가 발생했다.

**<font color='red'>"Error: ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client at Handshake.Sequence.\_packetToError"</font>**

---

`MySQL`에서는 보통 `'root'` 이외에 최종관리자 권한을 주지 않는 한 다른 계정으로 접속했을 때 그 계정에 권한이 없다.  
그러므로 `'dev'`라는 새로운 계정(유저)를 생성하고 DB 권한을 부여해줘야 한다.

구글링을 해보니 터미널로 설정하는 방법이 주를 이루어 여기서는 `Workbench`를 활용해서 더 간단하게 해결해보자.  
(터미널로 설정하는 법도 다루긴 한다.)

---

## Workbench로 새 계정에 Schema 권한 설정

`Workbench 접속`

#### 1. 계정(Account) 생성

<img width="80%" alt="스크린샷 2022-06-29 오후 9 36 33" src="https://user-images.githubusercontent.com/76654131/176439805-26c9ee7b-d050-46c5-bcb8-cd7cc36a8a12.png">

> MySQL에서 % 는 와일드 카드로 사용된다. <br> 서버와 같은 외부에서 허용하도록 하려면 host주소에 %로 지정해주면 된다.

<img width="80%" alt="스크린샷 2022-06-29 오후 9 37 53" src="https://user-images.githubusercontent.com/76654131/176439814-1d90e838-a4f2-45c4-a05b-cab494755464.png">

#### 2. Schema 권한 설정

<img width="80%" alt="스크린샷 2022-06-29 오후 9 38 19" src="https://user-images.githubusercontent.com/76654131/176439818-4ca0c2ee-963c-4426-9de3-942b842c4ec5.png">

<img width="80%" alt="스크린샷 2022-06-29 오후 9 38 43" src="https://user-images.githubusercontent.com/76654131/176439828-30eadb80-f525-4c71-918b-77d4baebab96.png">

<img width="80%" alt="스크린샷 2022-06-29 오후 9 38 59" src="https://user-images.githubusercontent.com/76654131/176439834-a64b677e-dc07-4be2-a1d5-953f1f303a79.png">

#### ✔️ 이렇게 하면 `Workbench`로 `dev`라는 새로운 계정(유저)를 생성하고 DB 권한을 부여해준거다.

---

`그럼 잠시 터미널로 설정하는 법을 알아보자.`

---

## 터미널로 새 계정에 Schema 권한 설정

터미널로 `mysql`에 접속해 아래와 같이 설정하면 위의 `Workbench`에서 설정한 것과 동일하게 설정되는데,

```shell
mysql> CREATE USER 'dev'@'%' IDENTIFIED BY '패스워드';

mysql> GRANT ALL PRIVILEGES ON *.* TO 'dev'@'%';

mysql> FLUSH PRIVILEGES;
```

❗️ 그런데 이렇게 터미널로 설정한 경우, `'dev'` 계정에 권한을 부여해줬음에도 불구하고,  
`MySQL 8.0`에서는 MySQL 패스워드 **플러그인** `caching_sha2_password` 때문에  
클라이언트 프로그램에서 사용하는 경우 <font color='red'>에러</font>가 해결되지 않고 그대로 발생한다.

```shell
$ SELECT Host,User,plugin,authentication_string FROM mysql.user;
```

<img width="545" alt="스크린샷 2022-06-29 오후 10 25 15" src="https://user-images.githubusercontent.com/76654131/176448403-61710ebb-c041-4295-863a-28b8cdf34260.png">

그래서 추가적으로 이렇게 `mysql_native_password` 플러그인으로 바꿔주야 정상 작동한다.

```shell
mysql> ALTER USER 'dev'@'%' IDENTIFIED WITH mysql_native_password BY '패스워드';
```

---

반면 `Workbench`를 이용해 위의 방법으로 설정하면, 자동으로 `mysql_native_password` 플러그인이 설정되어 정상 작동한다.

```shell
$ SELECT Host,User,plugin,authentication_string FROM mysql.user;
```

<img width="561" alt="스크린샷 2022-06-29 오후 9 41 10" src="https://user-images.githubusercontent.com/76654131/176439845-46094f33-1f75-46e2-9b18-a8b4bef6b3b4.png">

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://velog.io/@nari120/MySQL-ERNOTSUPPORTEDAUTHMODE-에러-해결](https://velog.io/@nari120/MySQL-ERNOTSUPPORTEDAUTHMODE-에러-해결)
