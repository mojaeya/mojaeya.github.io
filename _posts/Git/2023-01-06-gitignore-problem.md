---
layout: post
title: Git | .gitignore가 작동하지 않을 때
category: Git
tags: [git]
comments: true
---

<br>

가끔 브랜치에서 작업한 코드를 main으로 merge 하다가

gitignore가 제대로 작동되지 않아서 ignore 처리된 파일이 자꾸 changes에 나올 때가 있다.

이건 git의 캐시가 문제가 되는거라 아래 명령어로 캐시 내용을 전부 삭제후 다시 add . 해서 커밋하면 해결된다.

```cmd
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://jojoldu.tistory.com/307](https://jojoldu.tistory.com/307)
