---
layout: post
title: Vue.js | vue-cli npm install error (ERESOLVE could not resolve)
category: Vue.js
tags: [vue.js]
comments: true
---

> Vue.js 3.x / Vue-CLI 5

## 에러 발생

vue-cli로 프로젝트를 생성해서 셋팅을 마치고 전에 연습하던 프로젝트의 package.json에서 dependencies에 있는 라이브러리 파일들을 그대로 쓸거기 때문에 복사해서 옮겨줬다.

복사한 라이브러리들을 새 프로젝트에서 설치하기 위해 `npm install`을 해줬다.

원래 같았으면 `node_modules`가 생기면서 완료가 되어야 정상인데 이상한 오류가 발생했다.

<img width="579" alt="Screen Shot 2022-09-19 at 10 23 13 PM" src="https://user-images.githubusercontent.com/76654131/191167866-94b84303-c098-450d-961e-8feb215b77cb.png">

구글링 해보니 `Conflicting peer dependency` 즉, 특정 모듈이 다른 모듈과 함께 의존성을 가져야하는데 모듈간의 의존성이 없거나 안맞아서 발생하는 에러라고 한다.

## 에러 해결 1

`npm i --force` 또는 `npm i --legacy-peer-deps` 옵션을 추가하라고 하는데

- **--force** : 필요한 경우 패키지 의존성을 위해 추가적인 패키지를 설치
- **--legacy-peer-deps** : 그냥 무시하고 설치

나의 경우 `npm i --legacy-peer-deps` 옵션으로 해결이 되었지만 무시하고 설치한다는게 뭔가 찝찝했다.

## 에러 해결 2

`npm 7` 버전부터 생긴 이슈라고 하는데 난 현재 `npm 8` 버전이었다.

구글링 해보니 `npm 6` 버전으로 내리면 `npm install`로 정상작동 된다고 한다.

나는 혹시나 하고 일단 `npm 8` 에서 `npm 7`으로 내렸는데 정상작동이 되었다❗️

```cmd
$ sudo npm install -g npm@7
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> []()
