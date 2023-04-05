---
layout: post
title: [ITE4052]Regularization, Optimization
subtitle: Deep Learning Review
categories: ComputerVision
tags: [ComputerVision, ITE4052]
use_math: true
---
> 저번 글에서 최적의 W를 찾기 위해 Loss function으로 평가 하였는데,  
> 찾은 W가 너무 test set에 overfitting 될 수 있는 문제가 있음
> 이러한 문제를 해결하고자 나온것이 **Regularization**

## Regularization
Regularization의 키는 Simple model 만들기!


$$L(W) = \frac{1}{N} \sum_{i=1}^N L_{i}(f(x_{i},W), y_{i}) +  \lambda R(W) $$  


















