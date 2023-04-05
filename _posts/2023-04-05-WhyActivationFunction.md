---
layout: post
title: Activation Function 쓰는 이유
subtitle: 
categories: DeepLearning
tags: [DeepLearning, ITE4053]
use_math: true
---

## 활성화 함수

이전 layer의 값을 non-linear하게 변환하는 역할을 하고 이는 모델의 복잡도를 올린다.   
non-linear하지 않으면 아무리 layer 쌓아도 의미가 없다.    
($ \because f(ax+by)=af(x) + bf(y)$ 성질)    


### Regularization이 overfitting 막는 것과 연결되는 이유

결국 활성화 함수를 쌓아 non-linearlity를 이용해 복잡도를 올리는 것은 overfitting을 발생시킬 수 있는 것이다.   


![1][1] 

위의 tanh 함수를 보면 x값을 정규화 해준다면 0에 값이 가까워질것이다.

#### 수식으로 보면,   
$\lambda \uparrow　\Rightarrow　W^{[l]}\downarrow　\Rightarrow　z^{[l]}\downarrow　　　　(\because z^{[l]} = W^{[l]}a^{[l-1]}+b^{[l]})$    
　　　　　　　　　　　 $ \Rightarrow$ every layer　 $ \approx $　linear     
($\lambda$ : regularization parameter)   

#### 다시말해서,  
non-linearlity에 의해 복잡도가 올라가 overfitting 된 것을,   
정규화를 해주어 non-linearlity를 줄여 overfitting 예방.


[1]: https://github.com/yoominlee/img/blob/main/2023-04-05-WhyActivationFunction/1.jpg?raw=true


[출처1](https://ganghee-lee.tistory.com/30)   
[출처2]ITE4053 수업






