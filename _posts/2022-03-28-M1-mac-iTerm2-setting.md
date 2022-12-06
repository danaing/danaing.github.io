---
layout: post
title:  "M1 mac - 터미널 세팅하기 (iTerm2, oh-my-zhs)"
subtitle: iTerm2, Oh-My-Zhs로 편리한 개발환경 세팅하기
date:   2022-03-28
author: danahkim
categories: etc
tags: macOS
---

> 영롱하고 영리한 🍎 macOS 터미널을 만들어보자

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-01.png">

- **세팅 순서**
    1. iTerm2 설치
    1. oh-my-zhs 설치
    1. iTerm2 커스터마이징: 테마/폰트/컬러/상태바
    1. 플러그인 설치: 자동완성/하이라이터/Neofetch

- 2021년형 M1 Pro
- mac OS Monterey 기준

## 1. iTerm2 설치하기

macOS의 기본 터미널 대신 더 많은 기능을 제공하는 iTerm2를 많이 이용한다. 

[공식 홈페이지](https://iterm2.com/)에서 직접 다운받거나 아래 명령어를 쳐서 Homebrew를 통해 설치한다.

```console
$ brew install iterm2
```

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-02.png">

## 2. Oh-my-zhs 설치

macOS 기본 쉘이 bash에서 zsh(Z Shell)로 변경되었다. 여기에 더 다양하고 편리한 기능을 제공하는  ‘Oh-my-zhs’ 플러그인을 설치한다.

터미널이나 iTerm에 아래 명령어를 실행한다.

```console
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-03.png">

## 3. 커스터마이징

### 3.1. 테마 변경

- [테마 목록](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

테마 목록을 보고 바꿀 테마를 고른다. 오늘 변경할 테마는 **agonster**라는 테마로, 현재 checkout 중인 브랜치를 쉽게 알 수 있는 ~~국룰~~ 테마이다.

```console
$ open ~/.zshrc
```

에티터에서 ZSH_THEME 인 부분을 ZSH_THEME="agnoster"로 바꾸어준다

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-04.png">

### 3.2. 폰트 변경

테마를 바꾸고 iTerm2를 종료했다가 다시 실행하면 폰트가 깨져있다. 그래서 깨지지 않는 폰트로 변경한다. 나는 ~~역시나 국룰~~ 폰트 D2 Coding 글꼴을 설치한다.

- [D2 Coding 글꼴 다운로드 링크](https://github.com/naver/d2codingfont)

위 링크에 들어가서 zip파일을 다운받고 .ttf 파일을 눌러 서체를 설치해준다.

iTerm2를 켠 뒤 상태바 좌상단의 `iTerm2 > Preference > Profiles > Text > Font` 에서 다운받은 D2Coding 으로 폰트를 변경한다.

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-05.png">

참고로 원래 터미널도 폰트를 바꿔주어야 안깨지니 동일하게 바꾸어준다.

`터미널 > 환경설정 > 프로파일 > 서체`

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-06.png">

### 3.3. 컬러 변경

- [iTerm2 color shemes 다운로드 링크](https://iterm2colorschemes.com/)

설정에서 원하는 컬러 프리셋으로 변경할수도 있고, 아래 링크에서 많은 컬러 테마를 다운받아서 사용할 수 있다. 링크에서 zip파일로 다운받으면 schemes 라는 폴더 안에 .itermcolors 파일이 존재하고 이를 컬러 프리셋에 import 한다. 아래는 Atom이라는 컬러 프리셋이다. 참고로 최종 완성된 테마는 Snazzy를 사용하였다.

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-07.png">

`iTerm2 > Preference > Profiles > Colors > Color Presets > import` 에서 Atom을 import한다.

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-08.png">

원하는 테마를 클릭하여 변경한다.

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-09.png">

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-10.png">

컬러 적용 완료!

### 3.4. 상태바 추가

- 상태바 추가하기: `iTerm2 > Preferences > Profiles > Session > Status bar enabled`
- 상태바 위치 설정(bottom): `Preferences > Appearance > Status bar location > Bottom`

상태바를 클릭해서 아래처럼 원하는 메뉴를 놓는다. 

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-11.png">

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-12.png">

## 4. 플러그인 설치

터미널 대신 iTerm2를 쓰는 가장 큰 이유는 플러그인이다.

### 4.1. 자동완성 기능

예전에 사용한 명령어를 추천해주어 자동완성해주는 플러그인이다.

- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

아래 명령어를 실행해서 oh-my-zhs의 플러그인 디렉토리로 클론한다.

```console
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

open ~/.zshrc 에 아래 플러그인 경로를 추가한다.

```
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```

### 4.2. Syntax Highlighter

- [zsh-syntax highlighter](https://github.com/zsh-users/zsh-syntax-highlighting)

아래 명령어를 실행해서 oh-my-zhs의 플러그인 디렉토리로 클론한다.

```console
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

open ~/.zshrc 에 아래 플러그인 경로를 추가한다.

```
plugins=( 
    # other plugins...
    zsh-syntax-highlighting
)
```
<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-13.png">

### 4.3. Neofetch

-  [Neofetch 깃헙 링크](https://github.com/dylanaraps/neofetch)

화룡점정으로 영롱한 🍎사과 모양이 빠질 수 없다. Neofetch는 iTerm2 부팅 시에 사용자의 정보가 뜨도록 하는 플러그인으로 다양하게 커스터마이징이 가능하다. Neofetch 플러그인을 Homebrew를 통해 설치하고 terminal 실행 시 자동으로 실행되도록 `open ~/.zshrc` 을 입력해서 에디터로 맨 아래에 `neofetch`라고 한 줄 추가해준다.

```console
$ brew install neofetch
```

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-14.png">


## 😎 완성!!

<img src="/assets/images/M1-mac-iTerm2-setting/iTerm2-setting-01.png">

