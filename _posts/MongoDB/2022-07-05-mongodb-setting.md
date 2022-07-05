---
layout: post
title: MongoDB 설치 및 환경설정 (M1 Mac)
category: MongoDB
tags: [mongodb, mongodb compass]
comments: true
---

> M1 Mac / Homebrew

## Homebrew로 MongoDB 설치 및 실행

### `1. MongoDB tap 등록 및 확인`

```javascript
// 등록
$ brew tap mongodb/brew
```

```javascript
// 확인하는 방법 2가지
$ brew tap | grep mongodb
$ brew tap // 전체 탭 목록 출력
```

### `2. MongoDB 설치 `

```javascript
// 최신 버전의 mongodb 설치
$ brew install mongodb-community
```

### `3. MongoDB(mongod) 실행`

```javascript
// MongoDB 활성화
$ brew services start mongodb-community
```

📌 참고

```javascript
// MongoDB 비활성화
$ brew services stop mongodb-community

// MongoDB 재시작
$ brew services restart mongodb-community
```

### `4. MongoDB 접속`

`MongoDB`에 접속하려면 **`'mongosh'`**명령어를 사용한다. (`mongodb`는 기본적으로 TCP `27017`포트를 사용)

#### ✔️ 접속완료

```javascript
// MongoDB Shell(mongosh)은 기본적으로 'test' DB 사용
$ test > // 이렇게 뜨면 접속 완료
```

> 'mongo'는 이전버전 명령어로 'mongosh'로 대체(Superseded)된 후 차기 버전에서 삭제될 예정이므로 권장하지 않음.

---

# 환경설정

---

## 관리자 계정 추가 (모든 권한을 가진 root 권한 부여)

> 읽고 쓰는 권한을 가진 일반 사용자 계정도 만들 수 있다.

현재 상태로는 누구나 몽고디비에 접속이 가능하므로 관리자 계정을 추가해주자.

```javascript
$ use admin
$ db.createUser( { user: "이름", pwd: "패스워드", roles: ["root"] })
```

---

그런데 이렇게 추가해도 여전히 별도의 인증없이 몽고디비에 접속이 프리패스다.

#### 그래서 `Ctrl + C`를 눌러 쉘을 종료 한 뒤 몽고디비가 인증을 사용하도록 설정해줘야 한다.

---

## MongoDB 인증 기능 및 외부 접속 허용 설정

### `1. mongod.conf 파일 접근`

```javascript
// M1 Mac
$ vim /opt/homebrew/etc/mongod.conf

// Intel Mac
$ vim /usr/local/etc/mongod.conf
```

### `2. 보안 인증 기능 추가`

```javascript
...
security:
    authorization: 'enabled'
```

### `3. 외부 접속 허용 및 포트 번호 설정`

```javascript
// net 부분을 아래와 같이 변경
net:
    port: 27017
    bindIp: 0.0.0.0
```

#### ✔️ MongoDB(mongod) 서버 재시작 및 접속

```javascript
$ brew services restart mongodb-community
$ mongosh admin -u [이름] -p [패스워드]
```

---

### `MongoDB Compass`

- MongoDB에서 제공하는 GUI 환경의 MongoDB 클라이언트

설치는 MongoDB 공식 홈페이지에서 다운받아 설치하면 된다.  
[MongoDB Compass 설치](https://www.mongodb.com/try/download/compass)

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://velog.io/@fcfargo/TIL-MongoDB-Mongoose](https://velog.io/@fcfargo/TIL-MongoDB-Mongoose)  
> [https://seyslee.github.io/blog/installing-mongodb-on-m1-mac/](https://seyslee.github.io/blog/installing-mongodb-on-m1-mac/)
