---
layout: post
title: Dynamic Programming) Matrix-chain multiplication (4/4)
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---

## Dynamic Programming 
: 알고리즘의 한 종류.   
(메모리를 좀 더 쓰고 대신 시간 절약하는 방법중 하나)   
계산 결과를 저장해 두었다가 추후에 다시 사용.   
DP라는 이름과의 연관성 낮음

> 큰 문제를 작은 문제로 나눠 푸는 것.   
divide conquer와 비슷. 다만 작은 문제의 중복 유무가 큰 차이   
dynamic programming은 작은 문제들이 반복 O


Contents      
➖ Assembly-line scheduling    
➖ Rod cutting   
➖ Longest common subsequence   
☑️ Matrix-chain multiplication

## Matrix-chain multiplication

### 배경

두 행렬(matrix) A(pxq)와 B(rxs) 곱할 때,    
q=r이기만 하면 된다.    
최종적으로 pxs 크기 matrix 나옴.

다만, 여러 행렬을 곱할 때   
$(A_1\cdot A_2)\cdot A_3 = A_1 \cdot (A_2 \cdot A_3)$

위의 경우, 좌우 연산 결과는 동일하지만 연산량은 다르다.

![1][1]


### 문제 정의 

n 행렬의 chain $A_1, A_2, ... ,A_n$이 주어졌고, 각 $A_i$는 $p_{i-1}\times p_i$ 크기일 때,   
연산량이 최소가 되도록 하는 order 찾기   
어떻게 괄호 칠지


> ex) $A_1$  $A_2$  $A_3$  $A_4$는 다섯가지 방법으로 parenthesized 될 수 있다   
$A_1 (A_2(A_3 A_4))$,
$A_1 (A_2 A_3) A_4)$,
$(A_1 A_2)(A_3 A_4)$,
$(A_1 (A_2 A_3) A_4$,
$((A_1 A_2)A_3) A_4$


### Brute-force approach
: 비효율적

가능한 경우의 수 $P(n)$은,   

![2][2]

$= \Omega(4^n/n^{3/2})$


#### Dynamic programming

n개의 행렬의 곱이 주어졌을 때, 최적의 괄호 묶는 방법은, k와 k+1 사이에서 나누는 방법.    
또 1 ~ k, k+1 ~ n 두 chain에서 최적의 묶는 방법은 각각을 최적으로 나누기. ...   
=> 따라서 최적으로 묶는 방법은 부분을 최적을 묶는 문제로 나뉜다.

따라서 $m[i][j]$를 $A_i, A_{i+1}, ...A_j$의 최소 스칼라 곱연산 횟수라고 하자. 

![3][3]
위와 같이 정의 됨.

이 경우, 
- matrix $A_i$의 크기를 $p_{i-1}\times p_i$라고 하면, 

- $A_{i\cdot \cdot k} \times A_{k+1\cdot \cdot j}$의 연산 횟수는 $p_{i-1}p_kp_j$이다.

- s[i][j]는 최적(optimal)의 해를 tracing 할 수 있도록 optimal k를 저장








<동작방법 다시 붙여넣기>


















#### pseudo code
```c
MATRIX-CHAIN-ORDER (p)
    n= p.length−1
    let m[1 .. n][1 .. n] and s[1 .. n−1][2 .. n] be new tables 
    for i = 1 to n
        m[i][i] = 0
    for l= 2 to n                        // lis the chain length
        for i = 1 to n−l+1
            j= i+l−1
            m[i][j] = ∞
            for k = i to j−1 
                q= m[i][k] +m[k+1][j]+p[i−1]p[k]p[j]
                if q< m[i][j]
                    m[i][j] = q
                    s[i][j] = k
    return m and s
```

```c
PRINT-OPTIMAL-PARENS (s,i,j)   
    if i == j
        print "Ai" 
    else print "("
        PRINT-OPTIMAL-PARENS(s, i, s[i][j])PRINT-OPTIMAL-PARENS(s, s[i][j] +1, j)
        print ")"
```

#### Space consumption
table m과 s를 저장하기 위해서,   
$\theta(n^2)$

#### Running time
$\theta(n^2)$
![4][4]

||Space|Time|
|:---:|:---:|:---:|
|Assembly-line scheduling|$\theta(n)$|$\theta(n)$|
|Rod cutting|$\theta(n)$|$\theta(n^2)$|
|Longest common subsequence|$\theta(mn)$</br>$\theta(n^2)$|$\theta(mn)$</br>$\theta(n^2)$|
|Matrix-chain multiplication|$\theta(n^2)$|$\theta(n^2)$|



---

[1]: /assets/images/post_img/2023-10-31-AL_DynamicProgramming4/1.png
[2]: /assets/images/post_img/2023-10-31-AL_DynamicProgramming4/2.png
[3]: /assets/images/post_img/2023-10-31-AL_DynamicProgramming4/3.png
[4]: /assets/images/post_img/2023-10-31-AL_DynamicProgramming4/4.png

출처 : 2023-2 ITE2039 수업  

