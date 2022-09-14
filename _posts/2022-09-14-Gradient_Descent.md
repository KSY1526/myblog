---
toc: true
layout: post
description: boost
categories: [markdown, Gradient Descent]
title: Gradient Descent
---
# Gradient Descent 

## 백터 변수의 미분
###### 편의상 백터는 볼드체 소문자, 행렬은 볼드체 대문자로 표기합니다.
<br/> 

### $\partial _{x_i}f(\bold{x}) = \displaystyle\lim_{h\to0}\frac{f(\bold{x}+h\bold{e}_i)-f(\bold{x})}{h}$

<br/>
i번째 변수만을 편미분한 수식입니다.

$\bold{e}_i$ 벡터는 i번째 값이 1, 나머지 값이 0인 벡터로 i번째 변수만을 편미분 하기 위해 사용됩니다. 

### $\nabla f = (\partial_{x_1}f,\partial_{x_2}f,\partial_{x_3}f, ...)$

벡터 내 각 값마다 편미분 한 값을 다시 벡터 형태로 나타냅니다.

이 값이 
