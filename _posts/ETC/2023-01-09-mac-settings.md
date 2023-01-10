---
layout: post
title: Mac Settings
category: etc
tags: [etc]
comments: true
---

## 마우스 감도

#### 내가 쓰는 마우스 감도

`defaults write .GlobalPreferences com.apple.mouse.scaling 5`

#### 초기화

`defaults read .GlobalPreferences com.apple.mouse.scaling`

## Dock 자동숨김 애니메이션 속도 조절

#### Dock 자동숨김 && Dock 나타나기 시작할 때 딜레이 타임 조절 && 독이 나타나는 애니매이션 시간 조절

`defaults write com.apple.dock autohide -bool true && defaults write com.apple.dock autohide-delay -float 0 && defaults write com.apple.dock autohide-time-modifier -float 0 && killall Dock `

#### 초기화

`defaults delete com.apple.dock autohide && defaults delete com.apple.dock autohide-delay && defaults delete com.apple.dock autohide-time-modifier && killall Dock`

## 오른쪽 커맨드키 한영키로 전환하기 (앱 설치 X)

#### 1. hidutil 로 키매핑 매크로를 만든다.

```cmd
printf '%s\n' '#!/bin/sh' \ 'hidutil property --set '"'"'{"UserKeyMapping":[{"HIDKeyboardModifierMappingSrc":0x7000000E7,"HIDKeyboardModifierMappingDst":0x70000006D}]}'"'" \ >/Users/Shared/keymap

chmod 755 /Users/Shared/keymap
```

#### 2. keymap.plist 를 만들어 1번을 로그인때마다 실행하여 준다.

```cmd
cat<<: >/Users/Shared/keymap.plist

<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "[http://www.apple.com/DTDs/PropertyList-1.0.dtd](http://www.apple.com/DTDs/PropertyList-1.0.dtd)"><plist version="1.0"><dict><key>Label</key><string>keymap</string><key>ProgramArguments</key><array><string>/Users/Shared/keymap</string></array><key>RunAtLoad</key><true/></dict></plist>

:
```

#### 3. 매번 실행될수 있도록 2의 위치를 변경. 관리자 비밀번호가 필요하다.

```cmd
sudo mv /Users/Shared/keymap.plist /Library/LaunchAgents
```

#### 4. 정상적으로 작동하는지 확인

```cmd
launchctl load /Library/LaunchAgents/keymap.plist
```

#### 5. 키보드 단축키 변경

`설정 - 키보드 - 키보드 단축키 - 입력소스 - 입력 메뉴에서 다음소스 선택 단축키 오른쪽 커맨드 키로 변경`

#### 초기화

```cmd
launchctl remove keymap
rm /Users/Shared/keymap
sudo rm /Library/LaunchAgents/keymap.plist
```

## iterm + lsd 꾸미기

[https://gracefullight.dev/2019/05/27/install-lsd-on-mac/](https://gracefullight.dev/2019/05/27/install-lsd-on-mac/)
<br>
<br>
<br>

> **Reference**  
> 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.  
> 잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.  
> [https://vislog.tistory.com/entry/독Dock-자동숨김-애니메이션-조절제거하기](https://vislog.tistory.com/entry/독Dock-자동숨김-애니메이션-조절제거하기)  
> [https://www.youtube.com/watch?v=q-SOb9JHc3k](https://www.youtube.com/watch?v=q-SOb9JHc3k)  
> [https://www.notion.so/ee35e655235d41ecb259ff2f27ccb962](https://www.notion.so/ee35e655235d41ecb259ff2f27ccb962)
