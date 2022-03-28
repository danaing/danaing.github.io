---
layout: post
title:  "M1 mac - Jekyll blog 환경 세팅하기"
subtitle: 에러와 함께하는 Homebrew, Ruby, Jekyll 처음 설치하기
date:   2022-03-14
author: danahkim
categories: etc
tags: Jekyll Ruby macOS
---


> 맥린이의 에러와 함께하는 🍎 M1 mac에 Homebrew, Ruby, Jekyll 처음 설치하기

Apple Silicon을 오랫동안 눈여겨 보다가, 새로나온 M1 Pro를 드디어 구매했다. 따라서 이번 글은 오랫동안 Window만 사용하다가 처음으로 했던 <mark style='background-color: #fff5b1'> M1 Mac에서 Github blog 사용을 위한 설치 방법 </mark>에 대해 기록해두었다.

- 설치리스트
    - <mark style='background-color: #fff5b1'> Homebrew </mark>
    - <mark style='background-color: #fff5b1'> Ruby </mark>
    - <mark style='background-color: #fff5b1'> jekyll </mark>
- 2021년형 M1 Pro
- macOS Monterey 기준

## Jekyll blog란?

Jekyll은 정적 웹사이트 생성기로 Ruby 언어로 제작되었으며, 손쉽게 글을 쓸 수 있는 마크다운 글쓰기를 지원한다. GitHub Pages는 Jekyll로 구동되기 때문에 내가 원하는 사이트를 GitHub을 통해 무료로 만들 수 있다. 대부분 username.github.io라는 도메인으로 되어있는 테크 블로그가 그 예이다. 티스토리나 네이버블로그에 비해 원하는 대로 커스터마이징이 가능하고 다양한 테마를 쓸 수 있다는 엄청난 장점이 있다.

## Homebrew 설치하기

[Homebrew 홈페이지 바로가기](https://brew.sh/index_ko)

Homebrew는 macOS용(또는 Linux 시스템)에서 제공하지 않는 유용한 패키지 관리자이다. 홈페이지에 있는 명령어나 아래 명령어를 복사해서 터미널에 치면 Home Brew가 설치된다.

```console
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

password 입력창에 사용 계정의 비밀번호를 입력한다. 그리고 RETURN을 누르면 설치가 완료된다.

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-01.png"  title="untitled">

```console
Warning: /opt/homebrew/bin is not in your PATH.
  Instructions on how to configure your shell for Homebrew
  can be found in the 'Next steps' section below.
....
==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/awesome-d/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
- Run brew help to get started
```

그리고 아래처럼 PATH에 추가하라는 인스트럭션이 뜨면, 아래 두 줄을 추가로 터미널에 입력한다.

```console
$ awesome-d@Danah-MacBookPro ~ % echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/awesome-d/.zprofile
$ awesome-d@Danah-MacBookPro ~ % eval "$(/opt/homebrew/bin/brew shellenv)"                                                            
```

brew 명령어로 잘 설치가 되었는지 확인한다.

```console
$ awesome-d@Danah-MacBookPro ~ % brew --version                                                             
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-02.png"  title="untitled">

3.4.1 버전으로 설치가 완료되었다.

## Ruby 설치하기

[Ruby 공식 홈페이지](https://www.ruby-lang.org/ko/)

- `rbenv`란?  
[rbenv](https://github.com/rbenv/rbenv#readme)는 여러 종류의 Ruby를 설치할 수 있게 합니다. rbenv 자체는 Ruby 설치를 지원하지 않습니다만, [ruby-build](https://www.ruby-lang.org/ko/documentation/installation/#ruby-build)라는 유명한 플러그인에서 Ruby를 설치할 수 있습니다. rbenv, ruby-build 모두 macOS, Linux나 다른 UNIX-계열 운영체제에서 사용가능합니다.
- `ruby-build`란?  
 [ruby-build](https://github.com/rbenv/ruby-build#readme)는 다른 버전의 Ruby를 임의의 디렉터리에 컴파일하고 설치할 수 있게 하는 [rbenv](https://www.ruby-lang.org/ko/documentation/installation/#rbenv)의 플러그인입니다. ruby-build는 rbenv 없이 독자적으로 사용 할 수도 있습니다. macOS, Linux나 다른 UNIX-계열 운영체제에서만 사용 가능합니다.

macOS에서는 `rbenv`를 통해 Ruby를 설치한다. `rbenv`는 여러개의 Ruby 버전을 독립적으로 관리할 수 있도록 하는 패키지이다. 그리고 `ruby-build` 플러그인도 설치한다.

아래는 Homebrew의 `brew` 명령어를 이용하여 `rbenv` 와 `ruby-build`를 설치하는 명렁어다. 

```console
$ brew install rbenv ruby-build
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-03.png"  title="untitled">

아래 명령어를 통해 설치 가능한 Ruby 버전을 확인한다.

```console
$ rbenv install -l
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-04.png"  title="untitled">

Ruby는 최신 버전이 호환안되는 경우가 있기 때문에(에러의 원인 경우가 많았다ㅠㅠ) 안전하게 최신 버전보다 한두개 아래 버전을 설치할 것을 추천한다.

Ruby 원하는 버전을 아래 명령어를 통해 원하는 버전을 설치한다. 나는 `Ruby 2.7.5` 을 설치하였다.

```console
$ rbenv install {원하는 버전}
```

그리고 아래 명령어를 쳐서 설치된 버전을 확인해본다.

```console
$ rbenv versions
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-05.png"  title="untitled">

별(*) 표시가 system 앞에 설정되어있는 것을 알 수 있고 방금 설치한 2.7.5 버전이 보인다. rbenv global 버전을 2.7.5로 변경한다.

```console
$ rbenv global 2.7.5
$ rbenv rehash
```

버전을 다시 확인하면 2.7.5로 선택되어있다.

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-06.png"  title="untitled">

## Bundler 설치하기

이제 Ruby의 Gem을 통해 Bundler를 설치하려고 하면... 아래 에러가 뜬다.

```console
$ gem install bundler
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory.
```

system Ruby를 사용하고 있기 때문에 권한이 없다는 에러이다.
### rbenv의 PATH를 추가하여 해결하기

rbenv의 PATH를 추가해야한다. `echo $SHELL` 을 통해 M1의 기본 Shell을 확인한 뒤 zsh를 열어 설정을 변경해준다.

아래 명령어를 쳐서 .zsh 설정 파일을 연다.

```console
$ open ~/.zshrc
```

아래 두 줄을 추가해준다.

```console
export PATH={$Home}/.rbenv/bin:$PATH && \
eval "$(rbenv init -)"
```

(혹은 터미널에서 `vi ~/.zshrc` 을 입력한 뒤에 두 줄을 추가해주고, :wq 를 입력해서 나가도 된다.)

변경한 설정을 적용시켜주는 명령어를 입력한다.

```console
$ source ~/.zshrc
```

그리고 다시 Bundler 설치 명렁어를 치고 아래처럼 뜨면 성공이다!!

```console
$ gem install bundler
Fetching bundler-2.3.9.gem
Successfully installed bundler-2.3.9
Parsing documentation for bundler-2.3.9
Installing ri documentation for bundler-2.3.9
Done installing documentation for bundler after 0 seconds
1 gem installed
```

## Jekyll 설치하기

이번에는 jekyll을 설치에서.. 또 에러와 조우했다.

```console
$ gem install jekyll
Building native extensions. This could take a while...
ERROR:  Error installing jekyll:
	ERROR: Failed to build gem native extension.

    current directory: /Users/awesome-d/.rbenv/versions/2.7.5/lib/ruby/gems/2.7.0/gems/eventmachine-1.2.7/ext
/Users/awesome-d/.rbenv/versions/2.7.5/bin/ruby -I /Users/awesome-d/.rbenv/versions/2.7.5/lib/ruby/2.7.0 -r ./siteconf20220314-44873-emvjez.rb extconf.rb
.....
```

### Command Line Tools 재설치하여 해결하기

이유인 즉슨, XCode 업데이트 후 Command Line Tools를 설치하지 않았기 때문이라한다. 다른 블로그를 참고하니 Jekyll 설치하기 전에 처음부터 Command Line Tools 설치를 권장하고 있었다.

Command Line Tools를 설치하는 `xcode-select --install` 명령어를 치면 이미 설치가 되어있고 업데이트를 하라고 뜬다.

```console
$ xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

 그래서 아예 삭제하고 다시 설치한다.

```console
$ sudo rm -rf /Library/Developer/CommandLineTools
$ xcode-select --install
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-07.png"  title="untitled">

다시 jekyll을 설치한다

```console
$ gem install jekyll
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-08.png"  title="untitled">

jekyll 4.2.2 버전으로 설치 성공!

이제 cd로 디렉토리를 변경한 뒤 `jekyll new my-blog` 로 생성하거나, 원래 있던 프로젝트 폴더로 가서 아래 명령어로 bundler를 설치한다.

```console
$ bundler install
```

`localhost:4000` 로컬 환경에서 돌아가는것을 확인한다.

```console
$ bundle exec jekyll serve
```

<img src="/assets/images/M1-mac-jekyll-setting/jekyll-setting-09.png"  title="untitled">

드디어 jekyll blog 환경 세팅 끝!!!! 몇날 며칠 붙잡은 끝에 성공했다. Mac OS가 처음이라 하나하나 공부하고 검색하며 트러블슈팅하는데에 정말 오래 걸렸다.

편한 개발 환경과 터미널 커스터마이징의 필요성을 느껴서 다음은 iterm2와 Oh-My-Zhs를 설치하려한다.sss

## 기타 이슈

### brew로 install할 때 에러

```console
Cannot install under Rosetta 2 in ARM default prefix (/opt/homebrew)!
To rerun under ARM use:
    arch -arm64 brew install ...
To install under x86_64, install Homebrew into /usr/local.
```

brew 명령어 앞에 아래처럼 arch -arm64를 추가한다.

```console
$ arch -arm64 brew install rbenv
$ arch -arm64 gem install --user-install bundler jekyll
```

### 기존 프로젝트에서 jekyll 실행 시 Ruby 버전이 안맞는다는 에러

```console
rbenv: version `2.6.3' is not installed (set by /Users/awesome-d/Documents/GitHub/danaing.github.io/.ruby-version)
```

경로에 숨겨진 `.ruby-version` 파일을 찾아서 삭제해주었다.

## References

- Quick-start라고 하지만 전혀 Quick이 아닌 [Jekyll 공식 사이트](https://jekyllrb.com/)
- Ruby 환경변수 설정 트러블슈팅 참고 [향로님 블로그](https://jojoldu.tistory.com/288)