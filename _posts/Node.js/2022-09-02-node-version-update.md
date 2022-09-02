---
layout: post
title: Node.js | Version 업그레이드 하기
category: Node.js
tags: [node.js]
comments: true
---

> Mac OS

```javascript
// 버전 확인
$ node -v
```

```javascript
// 기존 npm 캐시 제거
$ npm cache clean -f
```

```javascript
// node.js 버전 관리해주는 'n' 모듈 글로벌 설치 *root 권한
$ sudo npm install -g n
```

- n stable : 안정 버전
- n latest : 최신 버전
- n lts : lts 버전
- n x.x.x : 특정 x.x.x 버전

```javascript
// 원하는 버전 설치 *root 권한
$ sudo n stable
```

```javascript
// 버전 확인
$ node -v
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://jsikim1.tistory.com/158](https://jsikim1.tistory.com/158)
