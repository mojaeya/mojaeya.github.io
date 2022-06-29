---
layout: post
title: MySQL 8.0 패스워드 초기화 (Mac)
category: MySQL
tags: [mysql]
comments: true
---

> MySQL 8.0.25 / Mac OS

`MySQL` **root** 패스워드를 까먹은 관계로 터미널에서 패스워드 초기화를 진행을 한 뒤, 새로운 패스워드를 설정해주었다.

난 참고로 이전에 `MySQL`을 homebrew로 설치 안하고 공식 홈페이지에서 다운받았다.

---

## 방법

1\. Mac 시스템 환경설정 - MySQL - `Stop MySQL Server` 클릭

---

2\. 서버 중지 후 터미널 창 **2개** 띄우기

---

3\. `A 터미널`에서 아래 코드로 안전모드 실행 (실행 시 요구하는 패스워드는 mac 자체 패스워드임)

```shell
$ sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
```

---

`A 터미널 그대로 냅두고,`

---

4\. `B 터미널`에서 아래 코드로 **mysql 접속**

```shell
$ sudo /usr/local/mysql/bin/mysql -u root
```

---

5\. 접속완료 뒤, 일단 아래코드로 `root 비밀번호 없애기`

```shell
$ UPDATE mysql.user SET authentication_string=null WHERE User='root';
$ FLUSH PRIVILEGES; // 현재 사용중인 MySQL의 캐시를 지우고 새로운 설정을 적용
$ exit;
```

---

6\. 다시 **mysql 접속**해서 `새로운 패스워드 설정`하기

```shell
$ sudo /usr/local/mysql/bin/mysql -u root
$ ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY '바꿀 비밀번호';
$ FLUSH PRIVILEGES;
$ exit;
```

---

7\. 마지막으로 **MySQL 서버 재시작**

```shell
$ sudo /usr/local/mysql/support-files/mysql.server restart
```

`B 터미널에서 재시작하면 A 터미널에서 실행했던 안전모드가 자동으로 종료된다. 그럼 끝!`

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://kwangkyun-world.tistory.com/entry/mysql-80-패스워드-변경-비밀번호-초기화-mac](https://kwangkyun-world.tistory.com/entry/mysql-80-패스워드-변경-비밀번호-초기화-mac)
