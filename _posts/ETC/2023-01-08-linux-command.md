---
layout: post
title: Linux 명령어
category: etc
tags: [etc]
comments: true
---

## rm (파일, 폴더 삭제)

- `rm [파일명]` - 파일 삭제
- `rm -f [파일명]` - 파일 강제 삭제

- `rm -r [폴더명]` - 폴더 삭제
- `rm -rf [폴더명]` - 폴더 강제 삭제

## tar (묶음, 압축)

#### tar 파일 묶기

- `tar -cvf [묶은 후 파일명.tar] [묶을 파일1] [묶을 파일2] .....`

#### 폴더 채로 파일 묶기

- `tar -cvf [묶은 후 파일명.tar] [묶을 폴더명]`

#### tar 파일 푸는 방법

- `tar -xvf [tar 파일명.tar]`

## cp (파일 복사)

- `cp [복사할 파일] [복사 후 파일명]`

## mv (파일,폴더 위치 이동 or 이름 바꾸기)

#### 파일,폴더 위치 이동

- `mv [파일명] [옮길 폴더명]`

#### 파일,폴더 이름 바꾸기

- `mv [기존 파일명] [새 파일명]`

## scp

> secure copy의 줄임말로 ssh를 이용하여 네트워크로 연결된 호스트간에 파일을 주고받는 명령어

[scp 명령어 사용법](https://eehoeskrap.tistory.com/543)

<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://jink1982.tistory.com/86](https://jink1982.tistory.com/86)  
> [https://bskyvision.com/943](https://bskyvision.com/943)  
> [https://eehoeskrap.tistory.com/543](https://eehoeskrap.tistory.com/543)
