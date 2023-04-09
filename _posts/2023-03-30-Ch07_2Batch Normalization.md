---
layout: post
title: -----DRAFT-----ITE4053_DL> 07-2 Batch Normalization 
subtitle: 
categories: DeepLearning
tags: [DeepLearning, ITE4053]
use_math: true
---

## Batch Normalization
: 굉장히 유명한 approach   
data augmentation 누구나 쓰듯 이것도!

- 하이퍼파라미터가 problem search 하는데 훨씬 쉽게함   
- Quick & better NN
- hyperparameter에따른 결과 차이 크지 않게 함.   
ex\) learning rate 0.1이나 0.2나 차이 크면 곤란   
but 이것 넣으면 차이 감소   

#### What is batch?
$X = [x^{1}  x^{2}  x^{3}   ...   x^{m} ]$ size (n,m)   
$Y = [y^{1}  y^{2}  y^{3}   ...   y^{m} ]$ size (1,m)   
vectorization은 효과적으로 m개의 train example 계산할 수 있게 함.

하지만 traning very slow.   
m개 각각 gradient 구해서 평균값으로 update 하는데, update 한번에 오래걸림.   
-> 이 문제 막고자 mini-batch 사용

#### Batch vs mini-batch
Batch: 한번에 전체 데이터 계산 후 update
mini-batch: 1000개씩 5000개의 mini batch 
$\therefore$ 한 batch(m개중에 1000개) 사용해서 gradient update

hyperparameter 빨리 업데이트할 수 있음

+ y(레이블)도 마찬가지로 동일한 크기로 나누는거 잊지말기

표기 알아두기
$x^{(i)}$ : ()소괄호는 training #   
$z^{[l]}$ : []대괄호는 layer #   
$X^{{t}}, Y^{{t}}$ : {}중괄호는 mini-batch #


#### One epoch
1000개씩 5000번 진행하는 mini batch가 있을 때   
1000개마다 업데이트 하는 것을 5000번 반복하면, train data 전체 한번씩 사용하는 것. => 1 epoch   

1epoch = 모든 데이터가 traning에 한번씩 노출되었다.

수업 중 Q.   
1000개 data(1 mini batch)써서 업데이트 하면, 다음 batch에 업데이트 된 W, b가 적용?
A. Yes 였던 것 같음

얼마나 오래 학습할 것인가에 대한 것인 epoch도 하이퍼 파라미터

#### Training with mini-batch gradient descent
![1][1]  

매번 step 마다 mini-batch 단위로 gradient 계산.    
이때 noisy 한 이유는,    
$\therefore$ 1000개에겐 gradient 감소지만 이후 1000개에겐 증가하는 방향일 수 있음.

noisy 하지만 크게 봤을 땐 감소하는 방향

#### Choosing your mini-batch size

![2][2]  

mini-batch size가,    
너무 작으면 -> 너무 noisy
너무 크면 -> 오래걸림    
중간크기가 best

![3][3]  

위 이미지에서 x표시 한 곳에서 학습 시작한다면, $M_{L}$ 로 수렴. ( $M_{G}$ 로 와야 하는데)   
하지만 Mini-batch 사용한다면, 가끔은 운좋게 Local에서 빠져나와  $M_{G}$ 로 갈수도 O
=> 가끔은 noisy한게 좋을 수도

Training set이 작다면 mini-batch가 아닌 그냥 batch gradient descent를 사용.   

mini-batch사이즈는:   
-> 64($2^{6}$), 128($2^{7}$), 256($2^{8}$), 512($2^{9}$), 1024($2^{10}$), ...   
2의 n승 크기로 보통 나눔. 
그래야 메모리에 더 잘 fit,   



수업 중 Q.   
mini-batch size라는게 데이터 총 크기? 개수?   
A. mini-batch size = number of set.


### Implementing Batch Norm
이전에 학습속도 올리고자 input을 normalization했었음.   
하지만 $W^{[l+1]}, b^{[l+1]}$ 학습 빠르게 하기 위해
input이 아닌 $a^{[l]}$ normalize할 수 없나?   
=> Batch Normalization (input이 아닌 feature map normalize)

이때, feature를 normalize하는데 z, a라는 선택지 2개가 있음.   
하지만 경험적으로 Z가 더 나았다.   
$\therefore$ 요즘 보통 z normalize  

















[1]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/1.jpg?raw=true
[2]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/2.jpg?raw=true
[3]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/3.jpg?raw=true
[4]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/4.jpg?raw=true
[5]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/5.jpg?raw=true
[6]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/6.jpg?raw=true
[7]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/7.jpg?raw=true
[8]: https://github.com/yoominlee/img/blob/main/2023-03-27-Ch07_1Problem%20Settings/8.jpg?raw=true



출처1 : 2023-1 ITE4052 수업  
[출처2](https://lsjsj92.tistory.com/391)   
[출처3](https://simsim231.tistory.com/93)   
[출처4](https://light-tree.tistory.com/125)   






