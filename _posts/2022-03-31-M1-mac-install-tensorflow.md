---
layout: post
title:  "M1 Pro에 TensorFlow2.X 설치 및 개발 환경 구축하기 (feat. Miniforge, GPU, VSCode)"
subtitle: Conda 가상환경으로 TensorFlow사용하고 VSCode와 연동하기
date:   2022-03-31
author: danahkim
categories: etc
tags: macOS TensorFlow
---

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-01.png" width='80%'>

이번 apple silicon을 구매하면서 가장 기대했던 부분은 M1 Pro칩에 **뉴럴엔진**으로 머신러닝의 연산 성능이 극대화되었다는 것이다. <mark style='background-color: #fff5b1; font-weight:bold;'>M1 Pro의 GPU를 사용하는 TensorFlow를 개발 환경 구축 과정</mark>을 기록해본다.

- 사양
    - macOS Monterey 12.3
    - M1 Pro - arm64(Apple Silicon)
    - **Miniforge 3**
    - **Python 3.8**
    - **TensorFlow 2.8.0**

## 가상환경이란?

일단 가상환경이 무엇인지 알아보자. 가상환경은 **독립적인 파이썬의 실행 환경**을 의미한다. 논리적으로 각자 다른 종류와 버전의 패키지를 가질 수 있는 환경이다. 프로젝트에 맞는 파이썬 환경을 구축하기 위해 필요한 패키지를 담아 놓는 바구니라고 생각할 수 있다.

그렇다면 가상환경을 왜 얘기하는 것일까? 예를 들어 **프로젝트A**에 필요한 패키지 버전과 **프로젝트B**에 필요한 패키지 버전이 다를 수 있다. 만약 버전이 다른데 하나의 환경에서 개발한다면 버전이 충돌하고 버그가 발생할 것이다. 그렇다고 프로젝트마다 버전을 upgrade하거나 downgrade해서 사용하는 것을 비효율적이고 또 다른 문제를 야기할 수 있다. 따라서 가상환경이 필요하며 TensorFlow에서도~~(다른 어디에서도)~~ 가상환경을 세팅을 권장하고 있다.

## Conda란?

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-02.png">

> ‘파이썬을 잡는데 도움이 필요합니다.’  
’가상 환경에 보관하십시오.’  (((아나콘다^^)))

Conda란 **가상환경을 통해 패키지 관리를 쉽게 해주는 도구**이다. 패키지 관리 시스템 conda를 통해 가상환경을 관리하는데 그 안에 필요한 패키지들을 설치하고, 그 가상환경 안에서 각 프로젝트가 다른 환경에서 작동하게 한다.

보통 아나콘다(Anaconda)라고 데이터 사이언스에 필요한 각종 패키지가 함께 설치되는 가상환경 관리 도구를 많이 사용한다. 나도 아나콘다를 먼저 검색해서 설치했으나, 도중에 TensorFlow가 되지 않아 중도에 포기하고 다른 방법을 찾아보았다.😭 아나콘다는 인텔 CPU까지만 지원하기에 Apple Silicon(M1)의 경우 아직 완벽히 지원되지 않는다고 한다.

## Miniforge 설치하기

따라서 Macbook M1 Pro(Apple Silicon)에서 TensorFlow를 사용하려면 Miniforge를 사용해야한다. Miniforge는 Apple Silicon의 arm64를 공식적으로 지원하는 Conda이다. Miniforge 공식 [링크](https://github.com/conda-forge/miniforge/)에서 파일을 다운받는다. 

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-03.png" width='80%'>

아래 명령어를 통해 다운받은 파일을 설치한다.

``` Console
$ cd downloads
$ bash Miniforge3-MacOSX-arm64.sh
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-04.png">

36개의 패키지가 설치됐다고 뜨면서 설치가 완료된다. (아나콘다는 300개 이상의 패키지가 함께 설치되는데에 비해 매우 약소한 패키지가 설치된다.)

## 가상환경 생성하기

Conda를 설치하고 터미널에 들어가면 앞에 (base)라고 뜨는 변화가 생기는데, 여기서 가상환경을 만들고 활성화시키면 그 가상환경이 괄호 안에 뜨게 된다.

Conda는 기본적으로 `conda`명령어를 통해 관리한다. 아래 명령어로 새로운 가상환경을 만든다. Python 버전은 3.8로 설치했다.

``` Console
# 관리중인 가상환경 정보
$ conda info --envs
# 새로운 가상환경 생성
$ conda create -n [가상환경명] python=3.8
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-05.png">

새로운 가상환경을 활성화시키고 설치된 리스트를 확인한다.

``` Console
$ conda activate [가상환경명]
$ conda list
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-06.png">

나중에 가상환경을 비활성화시킬때 사용하는 명령어이다. 

``` Console
$ conda deactivate
```

나중에 가상환경을 삭제할 때 쓰는 명령어이다.

``` Console
$ conda remove -n [가상환경명] --all
```

가상환경을 복제할 때 쓰는 명령어이다.

``` Console
$ conda create —clone [가상환경명] -n [새가상환경명]
```

## TensorFlow 설치하기

먼저 TensorFlow dependencies(tensorflow-deps)를 apple 채널을 통해 다운받는다. 

( -c [채널] [패키지] / -y: Do not ask for confirmation)

``` Console
$ conda install -c apple tensorflow-deps -y
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-07.png">

그 다음에 OS에 맞는 TensorFlow를 Python에 설치한다.

``` Console
$ python -m pip install tensorflow-macos
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-08.png">

마지막으로 M1에서 TensorFlow의 GPU를 지원해주는 Tensorflow-Metal plugin을 설치한다.

``` Console
$ pip install tensorflow-metal
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-09.png">

Jupyter Notebook의 차세대 버전인 Jupyter Lab을 설치해서 TensorFlow가 잘 구동이 되는지 확인해보자. 

``` Console
$ conda install -c conda-forge jupyter jupyterlab -y
$ jupyter lab
```

``` python
import tensorflow as tf
tf.__version__
tf.config.list_physical_devices()
```
<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-10.png">

M1 Pro에 **TensorFlow 2.8.0** 버전이 성공적으로 설치되었고 훈련 가능한 장치로 CPU와 GPU가 가능한 것을 볼 수 있다!!!👏

[텐서플로 2.0 시작하기 튜토리얼](https://www.tensorflow.org/tutorials/quickstart/beginner) 예제로 MNIST를 간단히 돌려보았다.

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-11.png">

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-12.png">

1분도 채 안걸려서 GPU로 잘 돌아갔다!!👏👏👏

## VSCode 가상환경 연동하기

이제 VSCode에서 가상환경과 연동해보자. 왼쪽에 확장을 누른 뒤 python을 검색해서 설치한다.

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-13.png">

왼쪽에 `설정 > 명령팔레트` 에서 `Python: Select Interpreter` 을 검색한다. 그리고 아래에 원하는 가상환경을 선택한다.

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-14.png">

왼쪽 아래 부분을 클릭하면 터미널 창을 켤 수 있는데, 아래처럼 (env-tf)라고 가상환경이 켜져 있는 것을 확인할 수 있다! 또는 터미널을 켜서 직접 아래처럼 입력해서 사용할 수도 있다.

<img src="/assets/images/M1-mac-install-tensorflow/tensorflow-15.png">

VSCode에서 가상환경 연동 완료! 이로써 M1 Pro에 GPU를 지원하는 TensorFlow 환경을 성공적으로 세팅했다!!🥳

## References

- 아나콘다 공식 블로그, Apple Silicon은 지원이 안된다는 슬픈 글: [‘**A Python Data Scientist’s Guide to the Apple Silicon Transition**’](https://www.anaconda.com/blog/apple-silicon-transition)
- 정말 구세주같은 영상 가장 도움이 많이 됐다(영어): **[How To Install TensorFlow 2.7 on MacBook Pro M1 Pro](https://www.youtube.com/watch?v=4nY5lDBXdOg)**
- 구세주같은 글, 벤치마크까지 흥미롭다: **[Apple Silicon M1 macOS에서 TensorFlow 활용기](https://cpuu.postype.com/post/9091007)**