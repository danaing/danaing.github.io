---
layout: post
title:  "TensorFlow Developer Certificate(텐서플로우 개발자 전문 자격증) 취득 후기"
date:   2021-06-30
author: danahkim
tags: TensorFlow
categories: etc
---

![image](https://user-images.githubusercontent.com/62828866/129131720-299a1329-c499-4834-aeec-13140d46db3b.png)

## 들어가며

안녕하세요. <mark style='background-color: #fff5b1'> <b> TensorFlow Developer Certificate </b> (텐서플로우 개발자 자격증)</mark>를 이번 6월에 취득하여 간단한 자격증 소개와 후기를 남겨보려합니다. 



## TensorFlow Developer Certificate이란?
먼저 TensorFlow Developer Certificate(텐서플로우 개발자 자격증)이란 Google에서 직접 공인하는 자격증입니다. 

![image](https://user-images.githubusercontent.com/62828866/129132700-428a7860-c7bb-447f-a09b-2cd32276fe48.png)

[TensorFlow 인증 프로그램](https://www.tensorflow.org/certificate)에 대한 자세한 설명은 위 공식 사이트를 참고하시면 됩니다.

본 자격증 시험에서는 **TensorFlow 2.x**를 사용하여 모델을 빌딩하여 문제를 해결하는 능력을 테스트합니다. 분야는 이미지, 자연어 처리, 시계열으로 다양합니다. 또한 사전 훈련(pretrained) 모델 사용 및 feature 추출, batch loading 이해, image augmentation 등 다양한 능력을 테스트합니다.
자격증의 유효기간은 3년이며, 자격증을 취득하면 [인증 네트워크](https://developers.google.com/certification/directory/tensorflow)에 자신을 TensorFlow 개발자로 등록할 수 있습니다!

![image](https://user-images.githubusercontent.com/62828866/129133169-e4993042-1d0b-403a-8df6-c0a914a89d35.png)



### 시험 구성
시험은 TensorFlow2.x를 사용하여 5개의 모델을 구현해야 합니다. 각각의 문제는 아래 카테고리로 구성되어 있습니다.

* 문제 구성
  * **Category 1**: <mark style='background-color: #fff5b1'>Basic / Simple model</mark>
  * **Category 2**: <mark style='background-color: #fff5b1'>Model from learning dataset</mark>
  * **Category 3**: <mark style='background-color: #fff5b1'>Convolutional Neural Network with real-world image dataset</mark>
  * **Category 4**: <mark style='background-color: #fff5b1'>NLP Text Classification with real-world text dataset</mark>
  * **Category 5**: <mark style='background-color: #fff5b1'>Sequence Model with real-world numeric dataset</mark>  
  ※ 각 카테고리당 90점 이상 합격

* 시험 환경: PyCharm IDE
* 시간: 최대 5시간
* 비용: 100 US 달러
* 합격 안내: 약 24시간 내

환경 세팅 및 응시 관련 자세한 내용은 [공식 수험자 가이드북](https://www.tensorflow.org/extras/cert/TF_Certificate_Candidate_Handbook_ko.pdf)를 참고하시면 됩니다.

특히 Anaconda 가상환경으로 환경을 설치하는 방법에 대한 정보는 [테디노트 유튜브](www.youtube.com/watch?v=2QCxK4OEiKc&t=396s)를 유용하게 참고하였습니다.


### 시험 준비
시험 설명이 잘 되어있어 준비에 특별히 어려운 사항은 없었습니다만 아무래도 주중에는 일을 병행하다보니 주말을 사용하여 1달 정도의 기간이 소요된 것 같습니다. 사실 마지막 1주일 정도 바짝 준비하였는데, 딥러닝에 대한 이해도와 환경에 따라 개인 별 시험 준비기간은 다를 것 같습니다.

본 자격증 취득을 위해 Coursera에서 무료로 수강할 수 있는 [DeepLearning.AI TensorFlow 개발자 전문 인증 과정](https://www.coursera.org/professional-certificates/tensorflow-in-practice) 강의가 있습니다. 2명의 강사가 나오는데 Google에서 AI Advocacy를 이끌고 있는 Laurence Moroney가 직접 DeepLearning과 TensorFlow에 대해 강의하시고, Stanford 대학의 유명 교수인 Andrew Ng 교수님이 담화에 나오십니다. 강의 자료와 설명도 매우 좋습니다. 1개의 강의 당 1주일동안 무료로 수강합니다. **이 강의에서 시험에 관련된 모든 내용을 거의 커버하고 또한 강의에서 나온 문제가 시험에 그대로 나오니** 강의 수강을 적극 권장드립니다. 만약 강의가 필요 없다면 위 강의의 [Laurence Moroney의 Github](https://github.com/lmoroney/dlaicourse) 활용하시면 데이터셋과 예제 그리고 과제의 답을 볼 수 있습니다.

저의 경우는 Coursera 강의 중에 필요한 부분을 들으면서, 깃헙에서 문제와 예제를 구해 스스로 모델을 여러개 만들어 각각의 성능을 개선하는 방법으로 공부하였습니다. **구글 Colab Pro 버전**을 사용하여 여러 모델을 만들었습니다. 


## 시험 후기

* **Category 1**
<mark style='background-color: #fff5b1'>Basic / Simple model</mark>  
주어진 벡터로 단순 선형 회귀 모델을 만드는 간단한 문제입니다. Dense 1개로 SGD와 MSE를 사용해서 모델을 만들었습니다.

* **Category 2**: <mark style='background-color: #fff5b1'>Model from learning dataset</mark>  
Fashion Mnist 데이터로 classification하는 문제가 나왔습니다. 저는 Conv2D와 MaxPooling2D를 연속적으로 사용하는 CNN 모델을 만들고 dropout으로 과적합을 방지하였으며, optimizer는 Adam을 사용하여 훈련하였습니다. Fashion Mnist는 class가 원핫인코딩이 되어있지 않으므로 Loss는 **Sparse categorical cross entropy**로 잘 설정해주는게 중요합니다. 

* **Category 3**: <mark style='background-color: #fff5b1'>Convolutional Neural Network with real-world image dataset</mark>
Horse or Humans dataset으로 말과 사람을 구분하는 분류기를 만드는 문제가 주어졌습니다. **ImageDataGenerator**를 사용해서 데이터에 랜덤한 변화를 주어 데이터를 증강하였습니다. 여기서 파라미터를 잘 주어야 성능이 올라갑니다. 그리고 모델은 pretrain된 **VGG16** 모델을 사용하였습니다.

* **Category 4**: <mark style='background-color: #fff5b1'>NLP Text Classification with real-world text dataset</mark>
RNN을 활용하는 텍스트 분류입니다. Sarcasm 데이터셋이 주어지고 **LSTM**을 사용한 NLP 모델을 만들었습니다. 

* **Category 5**: <mark style='background-color: #fff5b1'>Sequence Model with real-world numeric dataset</mark>  
시계열 데이터인 Sunspots가 주어지고 인공신경망을 사용해 시계열을 예측하는 문제입니다. TensorFlow에서 제공하는 함수로 **Window Dataset**을 만들어주고 LSTM 레이어를 쌓아서 신경망을 만들어주었습니다.


## 마치며

이번 자격증 취득을 통해서 TensorFlow 2.x에 대한 이해도를 높일 수 있었습니다. 사실 그보다 무언가 해냈다는 **자신감**과 자격증이 주는 **성취감**이 꾸준히 공부를 하는 긍정적 영향으로 동기부여가 되지 않을까 싶네요. 온라인 자격증 취득이 처음이다 보니 환경 세팅부터 이거저거 시행착오를 겪었지만 새롭고 즐거운 경험이었습니다.

소박하지만 이번 자격증 준비를 통해 느낀 점입니다.

1. Colab Pro에 무한한 감사를...  GPU가 없다면 ~~정신건강을 위해~~ Colab Pro사용은 선택이 아닌 필수입니다.
1. Callback 도 필수!
1. Dense 뿐만 아니라 Augmentation 각각의 parameter가 성능에 더 예민하다. 어떤 데이터로 train하느냐가 역시 더 중요한 것 같습니다.
1. 역시 Pretrained 모델이 성능이 막강하다는 것을 다시금 느꼈습니다. 제 경우에는 Google에서 만든 VGG Net을 사용하였고, 기존 CNN 모델에 비해 넘사 성능 개선을 하여 문제를 통과하였습니다.

시험이 끝나고 바로 합격 통지를 받았고, 당일 자격증을 발급 받았습니다. 이제 링크드인에 구글 텐서플로우 뱃지를 달 수 있겠네요!😆 자격증 취득만을 목적을 두지 않고 이미지, 자연어, 시계열 등의 다양한 분야와 모델을 익히는 것에 의의을 두고 단기 목표로 공부해보시면 좋을 것 같습니다.

![image](https://user-images.githubusercontent.com/62828866/129131796-8540df67-2f7d-4701-9710-94a911bc5bc6.png)

[TensorFlow Developer Certificate - Kim Dan Ah](https://www.credential.net/75d16cdd-ee28-4bc3-9222-59f0f87ee479)

