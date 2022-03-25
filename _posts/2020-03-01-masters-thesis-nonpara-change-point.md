---
layout: post
title:   Empirical Likelihood for Change-point Detection using Double Quantile (졸업연구논문)
subtitle: 석사 졸업 연구 논문
date:   2020-02-16
author: danahkim
tags: Nonparametric Change-point Graduate-school
categories: Statistics
---



졸업 논문이 본심을 통과하면서 2년의 석사 과정을 마치게 되었습니다. 제가 연구한 주제 **'Change-point detection using Nonparametric methods'**에 대해 적어보려 합니다.

* **논문**  
'Empirical Likelihood for Change-point Detection using Double Quantile' Danah Kim, Master thesis, Graduate School, Yonsei University, 2020  
→ [URL](https://library.yonsei.ac.kr/search/detail/CAT000001994068?briefLink=/main/searchBrief?q=%EA%B9%80%EB%8B%A8%EC%95%84)


* **통계학회 참여 및 수상 후기**  
→ [바로가기](https://danaing.github.io/statistics/2019/11/30/19-fall-statistics-conference.html)


## 1. Introduction

### 1.1. Backgrounds of Change-point Problem

<img src="/assets/images/master-thesis/2020-03-01-masters-thesis-nonpara-change-point-fde636c9.png" width="80%">
<center> <small> 나일 강의 연간 유량의 데이터로 점선이 change-point를 의미함.</small> </center> <br/>

먼저 **Change-point**란 단어 뜻 그대로 변화가 생기는 지점, 즉 **변동점**으로 시간의 흐름에 따른 일련의 과정에서 **근본적인 프로세스의 통계적인 속성이 변한 지점**을 의미합니다.

<img src="/assets/images/master-thesis/2020-03-01-masters-thesis-nonpara-change-point-controlchart.svg" width="70%">
<center> <small> sample의 평균값으로 그린 control chart 예시 (출처 1) </small> </center> <br/>


금융이나 제조업, 역학 등의 다양한 분야와 많은 실제적인 상황에서 통계학자는 **change-point가 발생했는지, 그리고 발생했다면 어디에 발생했는지**와 같은 문제에 봉착하곤 했습니다. [통계적 공정 관리(Statistical Process Control)](https://en.wikipedia.org/wiki/Statistical_process_control)의 아버지로 알려진 [W. A. Shewhart](https://en.wikipedia.org/wiki/Walter_A._Shewhart)는 1931년에 처음으로 불량률 관리의 측면의 Control Chart를 개발하였고, E. S. Page는 1954년에 변화를 탐지하기 위해 [CUSUM chart](https://en.wikipedia.org/wiki/CUSUM)를 고안합니다. 이러한 고민과 해결의 시도는 오래전부터 있었으며 이후 많은 연구들이 진행되었습니다.

<img src="/assets/images/master-thesis/2020-03-01-masters-thesis-nonpara-change-point-cusum.png" width="70%">
<center> <small> Threshold와 CUSUM chart 예시 (출처 2) </small> </center> <br/>



### 1.2. Change-point Problem

Change-point Probelm에 대한 정의는 다양합니다만, 여기서 우리는 Change-point problem에 대해 이렇게 정의하겠습니다.

Consider a sequence of
observations $x_{1}, x_{2}, \ldots, x_{n}$ drawn from independent random variables $X_{1}, X_{2}, \ldots, X_{n}$.  
Multiple $m$ change-points $\tau_{1}, \tau_{2}, \ldots , \tau_{m}$ exist in the data. Then there are $(m+1)$ segments.  
The distributions of the sequence can be written as

$$
X_{i} \sim
\begin{cases}
& F_{1} \; \; \; \; \text{ if $i \le \tau_{1}$} \\ 
& F_{2} \; \; \; \; \text{ if $\tau_{1} < i \le \tau_{2}$} \\ 
& \vdots \\ 
& F_{m+1} \; \text{ if $\tau_{m} < i$}
\end{cases}
$$


즉 Change-point문제는 Change-point $\tau$가 $\tau_{1}$ 부터 $\tau_{m}$까지 $m$개 존재할 때, $F_{1}$부터 $F_{m+1}$까지 $m+1$개의 distribution으로 나눠진다는 가정 하에 시작합니다. 이 때 distribution의 structure 변화는 주로 **평균**이나 **분산**의 변화 혹은 **분포**의 자체의 변화로 볼 수 있습니다. 그리고 이 Change-point problem에서 **$\tau$의 적절한 위치와 개수를 detect**해야 합니다.

### 1.3. Change-point Model

Change-point problem에서 **$\tau$** **의 적절한 위치와 개수를 detect하기 위한 통계적 모델**을 정의하겠습니다.  먼저 $\tau$에서 1개의 변화가 있다고 가정합니다. 이렇게 single change-point를 구하고, 나뉘어진 지점을 기준으로 앞 뒤로 **binary한 segmentation**을 연속적이고 반복적으로 수행하면 모든 change-point를 찾을 수 있습니다. 이를 표현하면 아래와 같이 single change-point를 detect하는 과정으로 단순화할 수 있습니다.

Consider independent random variables $X_{1} \sim G_{1},\ldots,X_{n}\sim G_{n}$.  
Assume that there is at most one change $\tau$ in the sequence of distributions above. We want to test the null hypothesis of no change

$$
\label{eq1}\tag{1}
\mathbf{H_{0}} : G_{1} = G_{2} = \ldots = G_{n} = F,
$$

against the following alternative of one change

$$
\label{eq2}\tag{2}
\mathbf{H_{a}} : F_{1} = G_{1} = G_{2} = \ldots = G_{\tau} \ne G_{\tau+1} = \ldots = G_{n} = F_{2}.
$$

where $1 \le \tau < n$ and neither F nor G is degenerate.
Using binary segmentation, it suffices to test and estimate the position of a single change point at each stage sequentially.


## 2. Proposed Methodology

### 2.1. Methods on change-point analysis

위에서 설명한 Model에서 change-point를 탐지하는 방법을 크게 통계적으로 **모수적 방법**과 **비모수적 방법**으로 나눌 수 있습니다. 모수적 방법 중 연구가 가장 많이된 분야는 정규분포에서 평균의 변화에 대한 탐지이며 또한 분산의 변화에 대해서도 연구가 되고 있습니다.  
그러나 모수적 방법에는 **(1)** <u>모수적 가정은 때때로 현실에서 만족되지 않으며</u> **(2)** <u>아웃라이어에 민감하고,</u> **(3)** <u>극단에 위치한 값은 분포에 따라 크게 다르다</u>는 한계점이 존재합니다.

그에 비해 비모수적 방법은 가정이 훨씬 적으며 다양한 상황에 더 적절하게 사용할 수 있습니다. 비모수적 방법으로도 change-point에 대해 많은 연구가 되었으며, 2007년의 Empirical likelihood ratio를 이용한 change-point문제에 대한 논문[^1]과 2017년에 제안된 Quantile empirical likelihood을 방법[^2]을 발전시켜, 이번 논문은 양 방향으로의 Double quantile empirical likelihood를 제안합니다.


### 2.2. Empirical likelihood

이 논문에서 이용한 비모수적 방법론은 **Empirical likelihood**입니다. [Art B. Owen](https://statistics.stanford.edu/people/art-b-owen)이 1988년에 비모수적 방법의 empirical likelihood를 처음 제시하였는데, 주요 아이디어는 각각의 관측치에 unknown probability mass를 주는 것입니다.

Assume that independently and identically distributed observation $x_{1}, ... ,x_{n}$ are from an unknown population distribution $F$. Let $p_{i} = P(X=x_{i})$. Empirical likelihood function of $ \{ p_{i} \}_{i=1}^{n}$ is defined as

$$
L(F) = \prod_{i=1}^{n} p_{i},
$$

where $p_{i}$ satisfy the constraints $p_{i} \ge 0$ and $\sum_{i=1}^{n} p_{i}=1$

그러면 $L(F)$는 $p_{i}=1/n$ 일때 가장 최대가 되며, Full model에서 $n^{-n}$를 최대값으로 가집니다.

When a population parameter $\theta$ identified by $E[m(X;\theta)]=0$ is of interest, the empirical likelihood maximum when $\theta$ has the true value $\theta_{0}$ is obtained subject to the additional constraint

$$
\sum_{i=1}^{n} p_{i} m(x_{i},\theta_{0}) = 0.
$$

관심있는 모수($\theta$)에 대한 제약식을 추가하여 likelihood를 최대화하는 각 observation에 대한 probability를 추정할 수 있습니다. 각각의 제약식을 라그랑주 승수법(Lagrange multiplier)으로 풀 수 있습니다.

To find $\{p_{i}\}_{i=1}^{n}$ under the restrictions, solve the Laglange Multiplier

$$
\sum_{i=1}^{n} \log p_{i} + \lambda_{0} ( \sum_{i=1}^{n} p_{i} - 1) +  \lambda_{1} (\sum_{i=1}^{n} p_{i} m(x_{i},\theta_{0})).
$$

따라서 아래처럼 Empirical Likelihood Ratio(ELR)를 구할 수 있으며, 이것은 근사적으로 Chi-squared distribution을 따른다고 알려져있습니다. Empirical Likelihood 방법은 Lagrange Multiplier Method를 사용하여 다른 제약식으로 확장하여 probability를 추정할 수 있습니다.

The Empirical Likelihood Ratio(ELR) statistic to test $\theta = \theta_{0}$ is given by

$$
\mathbf{R(\theta_{0})} = \frac{L(F)}{L(F_{n})} = \max \left \( \prod_{i=1}^{n} np_{i} | \sum_{i=1}^{n} p_{i}m(x_{i}, \theta_{0})=0, p_{i} \ge 0, \sum_{i=1}^{n} p_{i} =1 \right \)
$$

Under the null model $\theta = \theta_{0}$ with mild regular conditions, $-2 \log \mathbf{R(\theta_{0})} \to \chi_{r}^{2}$ in distribution as $n \to \infty$, where $r$ is dimension of $m(x, \theta)$ (Owen, 1988). The empirical likelihood method can be extended to other constraints using Lagrange multiplier method to find $\\{p_{i}\\}_{i=1}^{n}$.


### 2.3. Empirical Likelihood for Two groups comparison

위 검정 방법을 두 개의 그룹 비교 검정(Two groups comparison test)으로 확장할 수 있습니다. $F_{1}$과 $F_{2}$의 probabiity를 최대로하는 empirical likelihood를 정의하면, 아래와 같이 two sample test로 change-point를 binary하게 2개의 분포로 나누는 test와 동일하게 됩니다.


Two samples: $X_{1}, X_{2}, \ldots, X_{n} \sim F_{1}$ and $Y_{1}, Y_{2}, \ldots, Y_{m} \sim F_{2}$ and let $p_{i} = P(X=x_{i})$ and $q_{j} = P(Y=y_{j})$.
Empirical likelihood function of $p_{i}$ and $q_{j}$ is defined as

$$
L(F) = \prod_{i=1}^{n} p_{i}\prod_{j=1}^{m} q_{j},
$$

where $p_{i}$ and $q_{j}$ satisfy the constraints $p_{i} \ge 0, q_{j} \ge 0$ and $\sum_{i=1}^{n} p_{i}=1$, $\sum_{j=1}^{m} q_{j}=1$

This hypothesis (\ref{eq1}) and (\ref{eq2}) is equivalent to

$$
\mathbf{H_{0}} : F_{1} = F_{2},
$$

against

$$
\mathbf{H_{a}} : F_{1} \ne F_{2}.
$$

Thus, the hypothesis becomes two sample test.


### 2.4. Quantile Llikelihood Ratio for Two Sample

Zhou, Y., Fu, L., and Zhang, B.(2017) 논문에 따르면 여기에 Quantile을 이용한 constraints를 empirical likelihood에 추가하여 probability를 추정할 수 있습니다.

Under the null hypothesis, for any given $x$, we have $F_{1}(x)=F_{2}(x)=F(x)$. Let $p=F(\xi_{p})$; hence, $\xi_{p}$ is the $p$ quantile of $F$ and $\xi_{p}$ needs to satisfy

$$
\label{eq3}\tag{3}
    E[I(X_{i} \le \xi_{p})-p]=0, \quad \text{for } 1 \le i \le n+m,
$$
We can construct the following quantile empirical likelihood test statistic under restriction,

$$
\mathbf{R(\xi_{p})} = \max \left ( \prod_{i=1}^{n} np_{i} \prod_{j=1}^{m} mq_{j} | \sum_{i=1}^{n} p_{i} I(X_{i} \le \xi_{p}) ) = p,  \right .
$$

$$
\left . 
\sum_{j=1}^{m} q_{j} I(Y_{j} \le \xi_{p}) ) = p, p_{i}, q_{j} \ge 0, \sum_{i=1}^{n} p_{i} = \sum_{j=1}^{m} q_{j} =1 \right )
$$


이를 확장시켜 제가 제안하는 방법이 **Double quantile likelihood**입니다. 앞서보았던 empirical likelihood에 left side와 right side의 quantile을 constraints로 사용하여 추정하는 방법입니다. 2개의 quantile을 사용하여 Empirical likelihood를 maximize하는 것입니다.

Double quantile likelihood expand (\ref{eq3}) to $\textbf{Double quantile likelihood}$ for the both extreme side.
Let $p=F(\xi_{p})$ and $1-q=F(\xi_{1-q})$ ; hence, $\xi_{p}$ is the $p$ quantile of $F$ and $\xi_{1-q}$ is the $1-q$ quantile of $F$. This satisfies

$$
\label{eq4}\tag{4}
E[I(X_{i} \le \xi_{p})-p]=0, \quad E[I(X_{i} \ge \xi_{1-q})-q)]=0
$$

where $0 < p < 1-q < 0$ for $1 \le i \le n+m$.

Using (\ref{eq4}), double quantile empirical likelihood test statistic under restriction is

$$
\label{eq5}\tag{5}
\mathbf{R(\xi_{p}, \xi_{1-q})} = \max \left ( \prod_{i=1}^{n} np_{i} \prod_{j=1}^{m} mq_{j} | \sum_{i=1}^{n} p_{i} I(X_{i} \le \xi_{p}) )=p, \right .
$$

$$
\sum_{j=1}^{m} q_{j} I(Y_{j} \le \xi_{p}) )=p, \sum_{i=1}^{m} q_{i} I(X_{i} \le \xi_{1- q}) )=1-q, 
$$

$$
\left . \sum_{j=1}^{m} q_{j} I(Y_{j} \le \xi_{1-q}) )=1-q, p_{i}, q_{j} \ge 0, \sum_{i=1}^{n} p_{i} = \sum_{j=1}^{m} q_{j} =1  \right \)
$$

라그랑주 승수법(Lagrange multiplier)을 통해 유니크한 람다를 구하고 이로 확률을 추정합니다. 따라서 유도되는 DLR는 위와 같습니다. 이때 이 test statistic을 최대화시키는 사이p와 사이1-q를 택하고, 큰 test statistic Dn은 가장 가능성이 큰 적어도 하나의 change-point가 있다는 뜻으로 귀무가설의 기각을 의미합니다. 증명은 Appendix.A에 수록되어 있습니다.


Using Lagrange multipliers to solve (\ref{eq5}), we can get following unique $\lambda's$ and $p_{i}$ ,  $q_{j}$. (Proof in Appendix.A) This leads to double quantile likelihood ratio(DLR) test statistic.

$$
\begin{aligned}
\mathbf{R(\xi_{p}, \xi_{1-q})} = \left ( \frac{np}{n_{1}} \right )^{n_{1}} \left ( \frac{nq}{n_{2}} \right )^{n_{2}} \left ( \frac{n(1-p-q)}{n-n_{1}-n_{2}} \right )^{n-n_{1}-n_{2}} \\ 
 \left ( \frac{mp}{m_{1}} \right )^{m_{1}} \left ( \frac{mq}{m_{2}} \right )^{m_{2}} \left ( \frac{m(1-p-q)}{m-m_{1}-m_{2}} \right )^{m-m_{1}-m_{2}}
\end{aligned}
$$

where $\sum_{i=1}^{n} I(X_{i} \le \xi_{p}) = n_{1}$, $\sum_{i=1}^{n}I( X_{i} > \xi_{1-q}) = n_{2}$ and $\sum_{j=1}^{m} I(Y_{j} \le \xi_{p}) = m_{1}$, $\sum_{j=1}^{m}I( Y_{j} > \xi_{1-q}) = m_{2}$

$$
\therefore D_{n} = \sup_{\xi_{p}<\xi_{1-q}} \{ -2\log \mathbf{R(\xi_{p}, \xi_{1-q})} \}  
$$

Large values of $D_{n}$ indicate that there is at least one change-point.

## 3. Simulations

### 3.1. Algorithm for change-point detection

소개해드린 DLR로 change-point를 detection하는 알고리즘에 대해 말씀드리겠습니다. Change-point $\tau$는 two sample test인 DLR를 통해 추정이 가능합니다. 이때 F1과 F2의 sample size가 작다면 EL의 estimator인 람다는 존재하지 않을 수도 있으므로, $n$과 $m$의 샘플사이즈는 2007는 Zou의 논문에서 제시한 trimming 방법을 사용하여 조정된 $D_{n}^{\*}$ 를 구하고, 계산된 $D_{n}^{\*}$ 를 가장 maximize시키는 $\tau$를  $\tau$으로 추정합니다.

Change-point detection problem is to detect $\tau$ where

$$
F_{1} = G_{1} = G_{2} = \ldots = G_{\tau} \ne G_{\tau+1} = \ldots = G_{n} = F_{2}
$$

Two sample test: $X_{1}, \ldots, X_{n} \sim F_{1}$ and $Y_{1}, \ldots, Y_{m} \sim F_{2}$. When $n$ or $m$ is too small, the empirical likelihood estimators of $\lambda's$ may not exist. Therefore, use a trimmed statistic (Zou, C. (2007))

$$
D_{n}^{*} = \sup_{ c(n+m)^{-1/9}<\xi_{p}<\xi_{1-q}<1-c(n+m)^{-1/9} } \{ -2\log \mathbf{R(\xi_{p}, \xi_{1-q})} \}
$$

where $c$ is a positive constant.
The location $\tau$ can be estimated by

$$
\hat\tau = \arg_{\tau} \max \{ D_{n}^{*} \}
$$

### 3.2. Simulation

다음은 시뮬레이션입니다. Single change-point에 대해 시뮬레이션 수행하였습니다. 평균의 차이를 델타로 고정시키고 두 분포에서 observation값을 추출합니다. 그리고 change-point의 위치는 25%, 50%, 75%, 95%로 4개의 자리에 위치시켰습니다. 컴퓨팅을 고려하여 사이 $p$와 사이 $1-q$의 rank는 전체 샘플사이즈의 절반이상의 차이가 나도록 설정하였습니다. $D_{n}^{\*}$를 가장 크게 하는 $\tau$를 change-point로 택하는 시뮬레이션을 100번 수행하였습니다.

1. Assume that $X_{1}, ... ,X_{n}$ from $F_{1}$, and $Y_{1}, ... ,Y_{m}$ from $F_{2}$ with different distributions by setting $\delta$ satisfying $\delta=E_{F_{1}}(X)-E_{F_{2}}(X)$
1. Change location $m$ takes 25%, 50%, 75%, and 95% quantiles of the number of samples.
1. $\xi_{p}$ and $\xi_{1-q}$ are the value of $x's$ satisfying the rank($\xi_{p}$)-rank($\xi_{1-q}$) $\ge 0.5(n+m)$ for computation.
1. Calculate $D_{n}^{\*}$ and detect change-point $\hat\tau$.
1. For each case, 100 simulations are carried out.
1. Calculate the accuracy rate.


<img src="/assets/images/master-thesis/2020-03-01-masters-thesis-nonpara-change-point-d2fd887e.png" width="70%">

<img src="/assets/images/master-thesis/2020-03-01-masters-thesis-nonpara-change-point-143a683c.png" width="70%">
<center> <small> Simulation Results </small> </center> <br/>

시뮬레이션 결과 DLR이 전반적으로 다양한 분포와 여러 위치에 대해 전반적으로 괜찮은 성능을 보이는 것을 확인할 수 있습니다.

<img src="/assets/images/master-thesis/2020-03-01-masters-thesis-nonpara-change-point-12890a3a.png" width="100%">
<center> <small> DLR result: $\tau$=28, change-point=1898. </small> </center> <br/>

Change-point 분석에 널리 연구된 Nile 데이터에 실제 적용한 결과입니다. 왼쪽 plot은 DLR의 -2LLR입니다. max값인 28이 $\tau$로 추정되었습니다. 이는 오른쪽의 plot을 보았을 때, 1899년까지와 그 이후의 유량은 눈으로도 차이가 보이며 change-point를 잘 detect하고 있습니다. (논문에 따르면 1898년에 기후 변화와 nile강 주변 aswan dam의 개입으로 달라진것으로 보고 있습니다.) 추가적으로 Quantile이 1개일때와 2개일때의 Empirical CDF와 p-value에 대한 비교는 아래 첨부자료 Appendix.B를 참고하여 주세요.

본 연구는 예를 들어 제조업 공정, 기상 측정, 통화, 전력 등의 수요가 이상이 발생되어 후에 분포가 달라진다면 그 change-point를 찾을 수 있고 통계적 관점에서 해석이 가능합니다. 두 분포의 다름을 통계적 검정 방법으로 접근하고 이를 change-point로 바라보는 것에 의의가 있으며, 추후 알고리즘에 적용하여 연구 및 활용할 수 있다고 생각합니다. 긴글 읽어주셔서 감사합니다.


## References

* Chen, J. and Gupta, A. K. (2011). Parametric statistical change point analysis: with applicationsto genetics, medicine, and finance. Springer Science Business Media.
* Jing, B.-Y. (1995). Two-sample empirical likelihood method.Statistics & probability letters, 24(4):315-319.
* Owen, A. B. (1988). Empirical likelihood ratio confidence intervals for a single functional.Biometrika, 75(2):237-249.
* Owen, A. B. (2001). Empirical likelihood. Chapman and Hall/CRC. * Ross, G. J. and Adams, N. M. (2012). Two nonparametric control charts for detecting arbitrary distribution changes. Journal of Quality Technology, 44(2):102-116.
* Zhang, J. (2002). Powerful goodness-of-fit tests based on the likelihood ratio.Journal of the Royal Statistical Society: Series B (Statistical Methodology), 64(2):281-294.
* Zhang, J. (2006). Powerful two-sample tests based on the likelihood ratio.Technometrics, 48(1):95-103.
* Zhou, Y., Fu, L., and Zhang, B. (2017). Two non parametric methods for change-point detection in distribution.Communications in Statistics-Theory and Methods, 46(6):2801-2815.
* Zou, C., Liu, Y., Qin, P., and Wang, Z. (2007). Empirical likelihood ratio test for the change-point problem.Statistics probability letters, 77(4):374-382.

* **이미지 출처**
    * 1: https://en.wikipedia.org/wiki/Control_chart
    * 2: https://community.jmp.com/t5/JMPer-Cable/New-features-in-CUSUM-control-charts-for-JMP-16/ba-p/382920

----------------
2019년 10월 22일 연세대학교 대우관 본관에서 연구 논문의 예비심사가 진행되었으며 당시 발표에 사용한 자료를 첨부합니다.

<embed src="/assets/images/master-thesis/NP_cpt_Preliminary_Evaluation.pdf" type="application/pdf" width="600px" height="450px" />

----------------

