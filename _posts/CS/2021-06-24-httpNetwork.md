---
layout: post
title: HTTP 네트워크
category: CS
tags: [CS]
comments: true
---

# 네트워크
**네트워크**는 인간들이 흔히 카페에서 또는 sns로 소통을 하는 것처럼<br>**<font color='#1E90FF'>컴퓨터와 같은 단말들이 정보를 주고 받으며 공유하는 통신</font>**을 말한다.
 
하지만 단말마다 통신 방식이 다르기 때문에 규칙이 필요하다.
 
이 규칙을  통신 프로토콜(통신규약)이라고 부르고   
**네트워크**는 **<font color='#1E90FF'>"통신 프로토콜에 의한 단말 간의 통신"</font>** 이라고 풀어 설명 할 수 있다.
 
 프로토콜은 나중에 자세히 더 공부하겠지만 지금은 사전 그대로 규약 정도로 이해하고 넘어가자.

## 인터넷 

 
**인터넷**은 **TCP/IP** 기반의 **네트워크가 결합된 네트워크**다.
 
내가 아는 인터넷은 익스플로러인데 이게 무슨 소린가 싶었다.   
TCP/IP? 정보처리기사 필기를 딸때 무식하게 외우기만 했는데 이제는 제발 이해하고 넘어가자.

## TCP / IP 

- **서버**와 **클라이언트** 간의 데이터를 신뢰있게 전달하기 위해 만들어진 통신 규약
- 전송제어 프로토콜(**TCP**) + 인터넷 프로토콜(**IP**)로 이루어짐
- **IP 패킷**이라고 불리는 작은 조각을 통한 데이터 **전송**
- **TCP**는 **패킷**에 일련번호를 부여하여 데이터의 전달 순서를 **보증**
 
솔직히 설명하라면 못할 것 같다. 다음 장에서 정리해보겠다.

---

# HTTP
**인터넷의 멀티미디어 배달부 = Hypertext Transfer Protocol**
- 서버 / 클라이언트 모델
- 통신 종료 후 바로 연결을 끊는 비연결지향  /  연결 종료 후에는 상태를 유지 안하는 무상태
 
매우 쿨한 놈 나도 이별 후 http적인 인간이 되고 싶다.
 
하지만 재회하려면 연락이 필요하듯이 통신 종료 후에는 다시 연결하려면 리소스가 다시 필요하다.

이러한 단점을 보완하기 위해 나온게 [**쿠키와 세션 👈**](https://blog.naver.com/bohwajung/222233532663)
 

## HTTP 요청의 흐름

**" 브라우저가 서버로  Request  /   서버가 브라우저로 Response "**
 
## HTTP  메시지
<p align="center"><img width="80%"  src="https://user-images.githubusercontent.com/76654131/139288500-4fa74240-8f30-481d-a5ce-64153a59b86d.png"></p>

<br>

<p align="center"><img width="80%" src="https://user-images.githubusercontent.com/76654131/139288621-8eadcc2e-6187-48bc-9a18-ebaa4f36707d.png"></p>

 

## HTTP 요청 메서드
**서버에게 요청의 종류를 알리는 것**
- **GET** : 정보 요청 (select)
- **POST** : 정보 입력 (insert)  -> 주로 회원가입, 로그인 등 새로운걸 등록하는 것들
- **PUT** : 정보 수정(update)
- **DELETE** : 정보 삭제(delete)
 

## HTTP 응답 코드
- **100번대** : 요청을 받았으며 작업 계속 진행
- **200번대** : 요청을 성공적으로 받아들임
- **300번대** : 요청 완료를 위해 추가 조치 필요
- **400번대** : 요청의 문법 오류이거나 요청 처리  ->  프론트에서 먼저 문제 확인! 서버로 먼저 따졌다간 혼날수도
- **500번대** : 서버가 유효한 요청 응답 실패  ->  통상 서버쪽이 문제일 확률 높음

[**HTTP 상태 코드 👈**](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)

<p align="center"><img width="50%" src="https://user-images.githubusercontent.com/76654131/139288948-4f320975-1bf2-49e8-a320-ceab1e712d24.png"></p>
><center>여담이긴 한데,,,<br>  
오늘 회원정보 수정을 하는데 계속 이게 떠서 전화로 따졌는데 자기네는 문제가 없단다...<br> 
아무말도 못하고 이상한 숫자만 뜬다고 했는데...<br>
아는만큼 보이는것이 아닌, 아는 만큼 따질수 있다.</center>
  
---

## URL 구조

- 인터넷 상의 리소스 위치
- 특정 웹 서버의 특정 리소스에 접근 경로
- URI (Uniform Resource Identifier) : 식별자
- URL (Uniform Resource Locator) : 위치
- URN (Uniform Resource Name) : 이름

<p align="center"><img width="90%" src="https://user-images.githubusercontent.com/76654131/139289228-f429ab68-e504-488c-8599-04cc94c17bf0.png"></p>


- Scheme : 웹 클라이언트가 리소스에 접근하는 방식 ex) http, https(http 암호화 버전), ftp  
- Host : 서버의 위치
- Http 포트 기본값은 80, https 포트 기본값은 443이다. (포트 번호는 생략되는 경우도 있음)
- Path : 리소스의 경로
- Query : ?key=value 형식
 
<br>
<br>
<br>

>**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://blog.naver.com/qjawnswkd/222284233457](https://blog.naver.com/qjawnswkd/222284233457)