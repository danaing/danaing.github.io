---
layout: post
title:  2019년 추계 통계학술논문발표회 수상 후기
subtitle: Statistical Society Conference in Fall 2019
date: 2019-11-30
author: danahkim
tags: Conference Nonparametric Change-point
categories: Statistics
---


-----------

## 2019년 추계 통계학술논문발표회

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-06.jpg" width="80%">
<center> <small> 2019 한국통계학회 추계학술논문발표회 포스터 </small> </center> <br/>

2019년 11월 8일~9일 양일간 가을 한국통계학회에서 주최하는 학술논문 발표회 및 정기총회(줄여서 통계학술대회)가 서울시립대학교에서 열렸습니다. 저는 학생 포스터 논문 발표로 학회에 참가하였습니다.

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-08.PNG" width="80%">
<center> <small> 2019년 11월 8일 진행 일정 </small> </center> <br/>

포스터 논문 발표회는 미래관 101호와 103호에서 진행되었습니다. 자신의 연구와 논문을 포스터 형식으로 붙이고 참여한 학회원께서 자유롭게 보실 수 있습니다.

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-07.jpg" width="80%">

<center> <small> 포스터 세션 모습 스케치 (출처: 한국통계학회 홈페이지) </small> </center> <br/>

정말 다양한 연구 주제가 있습니다. 정해진 세션 시간에는 자유롭게 진행되는 논문 소개와 질의 시간이 있습니다.

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-01.jpg" width="80%">
<center> <small> 포스터 논문을 붙인 모습 </small> </center> <br/>

졸업 논문으로 쓰고 있던 **Nonparametric method for change-point detection based on empirical likelihood**(Empirical Likelihood를 사용한 변동점 탐지의 비모수적 검정 방법)이 그 주제입니다. 연구에 관련된 내용은 [여기](https://danaing.github.io/statistics/2020/02/16/masters-thesis-nonpara-change-point.html)를 참고해주세요.

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-02.jpg" width="80%">
<center> <small> 소개하는 포즈를 취해보았습니다 </small> </center> <br/>

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-03.jpg" width="80%">
<center> <small> 포스터 세션 중 논문을 설명하며 </small> </center> <br/>

위 사진으로 보시다시피, 예상보다 제 포스터에 관심있는 학회원분들이 많았습니다! 추측건대 통계를 공부하신 분들에게 **change-point**라는 제목이 큰 흥미를 끌었던 것 같습니다.
당시 학회원분들이 오실 때마다 저는 연구를 소개하였고, 주제에 관련한 여러 질의를 받았습니다. 또한 교수님으로 보이시는 평가관도 세션 시간에 저에게 질의를 하고 가셨습니다.


아래는 제가 받은 주된 질의와 답변입니다.
1. **기존 대비 얼마나 효과가 있는지?**

   "포스터의 시뮬레이션 결과를 참고하시면 알 수 있듯이, 다양한 상황 하에서 change-point를 더 정확하게 탐지합니다. (Accuracy가 높습니다.)"

1. **장/단점은 무엇인지?**

   "역시나 장점은 분포적 관점으로 접근하여 직관적이고 해석이 가능한 quantile을 사용한다는 이니다. 다만 이는 실시간 탐지가 아니라 사후 탐지이고, 시간을 희생하는 대신 정확도를 높였습니다. 또한 일변량이라는 단점이 있습니다."

1. **2개의 Quantile을 초기에 어떻게 세팅했는지?**

   "분포의 양 극단에 quantile값이 가지 않도록 극단을 제외하여 랜덤한 값으로 초기 세팅하고 step의 크기를 지정해줍니다."  
   $p = F(\xi_{p}), 1-q  = F(\xi_{1-q})$   $(\xi_{p} < \xi_{1-q})$

1. **이 방법론이 실제 어디에 활용될 수 있는지?**

   "change-point detection은 분포의 변화를 탐지할 수 있습니다. 예를 들어 제조업 공정, 기상 측정, 통화, 전력 등의 수요가 이상이 발생되어 후에 분포가 달라진다면 그 change-point를 찾을 수 있고 통계적 관점에서 해석이 가능합니다.  
   **두 분포의 다름을 통계적 검정 방법으로 접근하고 이를 관측치의 변동점으로 바라보는 것에 의의가 있으며, 추후 알고리즘에 활용하여 연구·적용할 수 있는데에 의의가 있다고 생각합니다.**"

외에도 많은 질문들이 있었습니다.


## 포스터 세션 후기

세션에는 정말 다양한 주제의 연구와 논문이 있었습니다. 또한 포스터 양식도 매우 다양했습니다. 역시나 한눈으로도 논문 전체를 금방 이해하시는 재야의 고수같으신 분도 계셨고, 정곡을 찌르는 날카로운 질문을 던지신 분도 계셨습니다. 생각보다 많은 분들이 통계를 공부하면서 열정을 가지고 연구하고 계시다는 것을 몸소 느끼는 기회였습니다.

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-04.jpg" width="80%">

<center> <small> 포스터 세션이 끝난 뒤 마무리하며 </small> </center> <br/>

마무리하면서 논문과 수식 그대로 제출하기 보다는 포스터에 과정을 조금 더 시각적으로 만들고, 흥미로운 dataset으로 illustration을 했으면 설명하기에도 더 좋았을 것 같다는 생각이 들었습니다.


## 포스터 논문상 수상

학술대회를 마치고 약 1달 후 발표회 수상자가 발표되었습니다. 저는 참여한 포스터 논문 발표 부분에서 예상치 못했던  **포스터 논문상 3등에 입상하였습니다!**

대학원 석사 과정에 진학하며 **통계 학술대회 참여하기** 라는 저만의 버킷리스트가 있었습니다. 2018년 부산대와 이화여대, 그리고 2019년 상반기 강원대에서 열렸던 매 학회에 참여하여 여러 강연을 들으면서 저도 나중에 리스너가 아니라 스피커의 입장으로 참여해보고 싶었는데, 드디어 버킷리스트를 이루었습니다.

졸업을 앞둔 바쁜 학기 중에 포스터를 만들어 직접 제작하기까지 여러 고충이 있었지만, 학계 분들 앞에 제가 그동안 노력했던 저의 결과물을 보일 수 있는 소중한 경험과 더불어 좋은 결과까지 얻게 되어 매우 뿌듯합니다!

<img src="/assets/images/19-fall-statistics-conference/19-fall-statistics-conference-05.jpg" width="80%">

<center> <small> 포스터 논문상 3등 수상 상장 </small> </center> <br/>

수상자에게는 위와 같은 상장과 소정의 상금이 수여됩니다.

## 포스터 논문

당시 제출했던 포스터 논문 파일을 첨부하니 참고해주세요.

<embed src="/assets/images/19-fall-statistics-conference/2019_2_poster.pdf" type="application/pdf" width="600px" height="900px" />



## 참고 사이트

* [사단법인 한국통계학회](http://www.kss.or.kr/)
* [2019년 추계학술대회 발표일정](http://www.kss.or.kr/bbs/board.php?bo_table=scheduleview&idx=129&mode=last)