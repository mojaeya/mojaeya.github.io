---
layout: post
title: Git | 한 컴퓨터에서 Github 계정 개인용/회사용 분리하기
category: Git
tags: [git]
comments: true
---

Github 회사 계정과 개인 계정을 한 컴퓨터 안에서 분리해서 사용해보자.

## 1. SSH key 생성

```javascript
// .ssh 폴더 생성 및 이동
$ mkdir ~/.ssh

$ cd ~/.ssh

// 개인용 ssh key 생성
ssh-keygen -t rsa -C “깃허브메일” -f personal
// 회사용 ssh key 생성
ssh-keygen -t rsa -C “깃허브메일” -f company
```

<img width="122" alt="스크린샷 2022-11-17 오전 8 53 24" src="https://user-images.githubusercontent.com/76654131/202320184-954d87de-1c66-457b-b32f-fabd8a1b5ebb.png">

- company -> 개인키 파일
- company.pub -> 공개키 파일

## 2. config 파일 생성

```javascript
// ~/.ssh 폴더에서
$ vim config

// 아래와 같이 작성
Host github.com-personal // 개인 계정
	HostName github.com
	User git
	IdentityFile ~/.ssh/personal

Host github.com-company // 회사 계정
	HostName github.com
	User git
	IdentityFile ~/.ssh/company
```

## 3. SSH Agent 등록

```javascript
$ ssh-add personal // 개인 계정 등록
$ ssh-add company // 회사 계정 등록

// 등록 확인
$ ssh-add -l
```

## 4. Github 계정에 공개키(\*.pub) 등록

```javascript
// 공개키 내용 그대로 전체 복사
$ cat ~/.ssh/company.pub
```

1. Github 프로필 > Settings > SSH and GPG keys > New SSH key
2. Key에 복사한 ssh 공개키 붙여넣기

## 5. 연결 테스트

```javascript
$ ssh -T github.com-company
```

## 6. Repository Clone 하는 방법

- 기존에 글로벌로 개인 계정을 등록해놨으면,

  - `SSH 을 누르고 주소 복사 * 기본 경로 git@github.com:[user]/[저장소]`

- 회사 계정으로 할 경우, 기본 경로를 내가 지정해준 회사용 Host 명으로 바꿔서
  - `git@github.com-company:[user]/[저장소]`

## 7. 특정 폴더에서 회사 계정으로 푸시하게 만들기

ex) ~/Documents/Company 라는 폴더(디렉토리)에서는 회사 계정으로 커밋 & 푸쉬가 되게 하기.

```javascript
$ vim ~/.gitconfig

// 아래와 같은 내용 추가
[includeIf "gitdir:~/Documents/Company/"]
        path = ~/Documents/Company/.gitconfig-company
```

#### ❗️ ~/Documents/Company 폴더 안에서

```javascript
$ cd ~/Documents/Company

// 위의 path 이름으로 된 gitconfig 파일 생성
vim ~/.gitconfig-company

// 아래의 내용 입력
[user]
	email = 회사 계정 이메일
	name = 회사 계정 이름
```

`~/Documents/Company` 아래에 Git 저장소를 초기화하거나 클론하고 커밋에 기록되는 사용자 정보를 확인 했을 때,  
회사 계정 메일과 이름이 뜨면 성공이다.

```javascript
$ git config user.email
$ git config user.name
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://nareunhagae.tistory.com/71](https://nareunhagae.tistory.com/71)
