---
layout: post
title: 3.4.2 Association Rules
subtitle: Chapter5, Mining Frequent Patterns, Association and Correlations
categories: DataScience
tags: [DataScience, ITE4005]
use_math: true
---

지금까지,    
많은 pattern mining 공부.   
ex\) basic apriori & its extensions(sampling, partition, hash base method ... ), FP-growth algorithm

이번 챕터,   
~~Apriori와 관련된 더 많은 extension,~~(이전 post)   
Association rule mining과 관련된 더 많은 concept에 대해

#### 목차

1. Mining multilevel association   
2. Mining multidimensional association   
3. Mining quantitative association    
4. Mining interesting correlation patterns   


## 1. Mining multilevel association   

### 사용 이유

> 보통 마트의 물건은 hierarchy를 가진다.   
> 예를 들어, 우유라는 카테고리 안에 2% milk와 skimed milk 두 종류가 있다.    
> 이런 item의 hierarchy를 고려하기 위해서는 minimum support를 계산할 때 flexibility가 있어야 한다.


### 특징

- Lower level은 lower support   
  
- lower-level 아이템과 higher-level 아이템의 frequent pattern에 포함될 확률을 최대한 비슷하게 한다.   

- uniform setting: hierarchy고려 없이 전체 itemset에 동일한 min_support적용   
flexible setting: higher-level에는 높은 min_support, lower-level에는 조금 낮춘 min_support 


### Redundancy problem

> 위에서 본 lower-level에는 조금 낮춘 min_support 적용 시 Redundancy problem이 발생할 수 있다.   

- higher level rule에 이미 lower level rule 포함할 수 O.   

#### descendent(자손) rule이 (불필요) 할 조건
- support가 (ancestor rule's support value에 기반한)expected value에 가깝다   
- confidence가 ancestor rule에 가깝다   

#### 예시

![1][1]  

위와 같은 경우, <u>첫번째 rule이 두번째 rule의 ancestor라고 한다.</u>

---

2% milk의 support가 2%라면,

우유의 25%가 2% milk인 경우\)   
milk의 expected value는 x4인 8%.   
-> "expected" 이므로 descendent 지우고 ancestor만 남긴다.

우유의 60%가 2% milk인 경우\)   
milk의 expected value는 3.6%정도.   
$\therefore$ 둘 다 중요 -> redundant 하다고 하지 않는다.



## 2. Mining multidimensional association   


![2][2]  

























[1]: https://github.com/yoominlee/img/blob/main/2023-04-04-2AssociationRules/1.jpg?raw=true
[2]: https://github.com/yoominlee/img/blob/main/2023-04-04-2AssociationRules/2.png?raw=true




---

출처 : 2023-1 ITE4005 수업  





