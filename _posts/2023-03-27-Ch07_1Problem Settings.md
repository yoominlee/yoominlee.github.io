---
layout: post
title: Problem Settings
subtitle: 07 Problem Settings
categories: DeepLearning
tags: [DeepLearning, ITE4053]
---

## Problem Setup

### Applied ML is a highly iterative process

- NN 학습시, 많은 결정을 내려야 한다:
    - 레이어의 수
    - hidden unit의 수
    - learning rate
    - activation function 등

- 한번에 hyperparameter들에 맞는 값을 찾는 것은 거의 불가능하다.

- 따라서 machine learning은 매우 반복적인 작업.

### Dataset
: 모델 만들 때 데이터 나누어 사용

- Traning sets
    : unknown 변수 update 하는데 사용
    : (지금까지는 trainset만 가지고 이야기 했음)
- development sets
    : evaluate(잘하고 있다, 아니다 평가용도)   --?
- test sets 

결과에 매우 중요

### Train/Dev/Testset

" 어떻게 나눌 것인가 하는 문제 "

rule of thumb for splitting data
- previous era (# of samples = 100 or 1000 or 10000)
    training/test = 70/30 %
    training/dev/test = 60/20/20 %
- big data era /(# of samples = 1,000,000) : 양 많은 경우
    training/dev = 99/1 %

-> 데이터셋 양이 적은 경우 test set 비율 ⬆️ 

-> 데이터셋 양이 많다면 test set 비율 ⬇️


### K-Fold Cross-Validation

: 적은 수의 데이터셋 있는 경우
시스템의 퍼포먼스 체크하는용으로 사용

단계\)
1. K개로 data set 나눔 (typically K = 5 or 10)
2. K개의 덩어리 중 첫번째 것을 test set으로 두고, K-1개를 가지고 network train.
3. 두번째 덩어리를 test set으로 두고 반복.
4. 덩어리 바꾸며 train 하는 것을 K 회 반복. (train 할 때마다 W, b 업데이트)
5. K test error(loss/cost) 평균 내서 estimated test error 얻음


### Mismatched train/test distribution
: distribution이 같아야 한다.

검은 고양이 학습하면 test set의 흰 고양이 찾기 힘들꺼임
-> distribution이 다름

rule of thimb for splitting data:
- dev와 test set 같은 distribution
- test set 가지지 않는것 괜찮을 수 있다. (only dev set)

### Bias and Variance 

- bias와 variance는 tradeoff 관계.(하나 좋게 하면 하나 안좋아지는 관계)
- 최근에 deep learning era에서는 중요도 조금 줄었음
![1][1]  

- high bias
    - under fitting



[1]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/1.jpg


출처1 : 2023-1 ITE4052 수업  
[출처2](https://lsjsj92.tistory.com/391)







