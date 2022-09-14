---
toc: true
layout: post
description: 부스트캠프 1주차 경사하강법 소개.
categories: [BoostCamp, Gradient Descent, math, markdown]
title: "[BoostCamp]Gradient Descent"
---
# 경사하강법 (Gradient Descent)

## 백터 변수의 미분 

*볼드체 소문자는 벡터, 볼드체 대문자는 행렬을 의미합니다.*


$\partial_{x_i} f(\bold x) = \displaystyle\lim_{h\to 0}\frac{f(\bold x+h\bold e_i)-f(\bold x)}{h}$

i번째 변수만을 편미분한 수식입니다.

$\bold{e}_i$ 벡터는 i번째 값이 1, 나머지 값이 0인 벡터로 i번째 변수만을 편미분 하기 위해 사용됩니다. 

<br/>

$\nabla f = (\partial_{x_1}f,\partial_{x_2}f,\partial_{x_3}f, ...)$

벡터 내 각 값마다 편미분 한 값을 다시 벡터 형태로 나타냅니다.

이 벡터를 '그레디언트 벡터'라고 부르며 경사하강법에 직접 사용됩니다.

<br/> 

## 경사하강법의 기초 원리

한 점의 미분값은 함수가 증가할때는 양수, 감소할때는 음수로 나타납니다.

이 성질을 이용해 특정 위치에서 함수 내 극솟값을 찾기 위해선 그 위치의 미분 값에서 빼는 연산을 하면 됩니다.

극솟값은 x의 미분값이 양수이면 x가 더 작은 값을 가질 것이고 음수이면 x가 더 큰 값을 갖기 때문입니다. 또 극솟값의 미분 값은 0이구요. 

벡터로 확장하면 특정 위치의 벡터에서 앞서 구한 그레이던트 벡터를 빼는 연산을 하면 됩니다.

<br/> 

## 선형회귀에서의 경사하강법

$\nabla _ \beta {(\bold y - \bold X\beta)}^2 =(\partial_ {\beta _1} {(\bold y - \bold X\beta)}^2, \partial _ {\beta _2} {(\bold y - \bold X\beta)}^2, ..., \partial _ {\beta _d} {(\bold y - \bold X\beta)}^2)$

앞 벡터 중 k번째 값을 뽑으면, 


$(\displaystyle\frac 1 n\displaystyle\sum_{i=1}^{n}$

$(y_i-\displaystyle\sum_{j=1}^d X_{ij}\beta _j)^2)={\partial_{\beta_k}}$

$\partial_{\beta _k}$

$(y_i-\displaystyle\sum_{j=1}^d X_{ij}\beta _j)^2)$

$\partial_{\beta_k} (\bold y - \bold X\beta)^2 = \partial_{\beta _k} (\displaystyle\frac 1 n\displaystyle\sum_{i=1}^{n}(y_i-\displaystyle\sum_{j=1}^d X_{ij}\beta _j)^2) = \partial_{\beta _k} (\frac 1 n \displaystyle\sum_{i=1}^{n}(y_i^2-2y_i\displaystyle\sum_{j=1}^d X_{ij}\beta _j + (\displaystyle\sum_{j=1}^d X_{ij}\beta _j)^2))$

$=\displaystyle\frac 1 n \displaystyle\sum_{i=1}^{n}(-2y_iX_{ik}\beta_k +2X_{ik}(\beta_1X_{i1}+\beta_2X_{i2}+ ... + \beta_dX_{id})) =-\frac 2 n(\beta_k\displaystyle\sum_{i=1}^{n}(y_iX_{ik}) - \displaystyle\sum_{i=1}^{n}X_{ik}(\bold X_{i.} \bold\beta))$

$= \displaystyle -\frac 2 n(\bold X_{.k}^T\bold y - \bold X_{.k}^TX_{i.}\bold\beta)$

데이터 개수가 총 n개, 종류가 총 d개 입니다. 포인트는 베타k로 편미분 되는 사실을 잘 기억하고 시그마 내에 미분 연산을 집어넣는 것 입니다.

선형회귀에 경우 볼록함수로 극솟값이 하나만 존재하고 전역 최솟값인 것이 보장됩니다.

다만 앞으로 다룰 목적함수들은 볼록함수가 아닐 가능성이 높습니다. 즉 극솟값이더라도 최솟값임을 보장할 수  없습니다.

<br/> 

## 확률적 경사하강법(SGD)

미분 가능하고 볼록한 함수에서는 경사하강법이 최솟값을 찾는 것이 보장됩니다.

하지만 거의 모든 딥러닝 손실함수는 비선형함수 입니다. 극솟값이 전역 최솟값을 보장하지 못합니다.

즉, 최솟값을 구해야 하나 극솟값에 잘못 수렴할 수 있습니다.

또 정말 많은 데이터와 파라미터를 다루는 경우 컴퓨터의 메모리 문제도 존재합니다.

따라서 모든 데이터를 활용해서 파라미터를 업데이트 하는 대신 하나 혹은 일부 데이터를 사용하는 확률적 경사하강법을 주로 사용합니다.

확률적 경사하강법(SGD)는 모든 데이터를 사용하지 않기 떄문에 목적식이 약간 달라집니다.

그러므로 극솟값에서의 미분값이 경사하강법과 다르게 0에 가까울 뿐 0이 아닐 가능성이 높습니다.

즉, 극솟값에서 탈출할 수 있습니다. 극솟값에 머무르지 않는고 전역 최솟값으로 나아갈 수 있다는 얘기죠.

또 연산자원을 효율적으로 사용할 수 있습니다. 큰 데이터를 다루는 대도 문제가 없습니다.

다만 너무 작은 개수의 데이터를 사용하면 경사하강법 목적식을 많이 왜곡하므로 이를 지양해야겠습니다.

<br/> 

## 간단한 후기

경사하강법의 개념을 모르진 않았는데 제가 부족한 것을 많이 배운 것 같습니다.

더 많은 내용이 있으나 다 기록하기에 힘이 붙여 저한테 중요한 포인트만 적어봤습니다.

앞 기수에서 배운 내용을 블로그에 기록하는 것을 보고 정식시작 전 저도 연습 겸 했습니다.

마크다운 언어를 직접적으로 사용한 것은 처음인데 생각보다 어렵네요. 특히 수식이 많이 까다로웠습니다.

그래도 익숙해질 겸 미리 경험한 것이 좋았습니다.
