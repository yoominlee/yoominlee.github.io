---
layout: post
title: Insertion Sort
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---

### Sorting 문제란,

Input: n개의 숫자의 시퀀스 $<a_1, a_2, a_3, ... ,a_n>$ = keys 

Output: $a'_1 \le a'_2 \le ... \le  a'_n$을 만족하는 input 시퀀스의 재배열


# Insertion Sort
: insetion을 사용하는 정렬 알고리즘

### insertion이란,
key와 정렬된 list의 key들이 주어지고, 정렬 유지하며 list에 key를 넣는것


## 동작 예시

5 2 4 6 1

<u>**5**</u> 2 4 6 1

<u>**2 5**</u> 4 6 1

<u>**2 4 5**</u> 6 1

<u>**2 4 5 6**</u> 1

<u>**1 2 4 5 6**</u>


## Pseudo Code
<pre>
<code>
for j=2 to A.length
    key = A[j]
    i = j-1     // 뒤에서부터 찾아감
    while i>0 and a[i]>key
        A[i+1] = A[i]
        i=i-1
    A[i+1] = key
</code>
</pre>


각 줄 마다 cost 생각해보면,

line1: n    (2~N+1 $\because$ N+1의 경우 반복문의 조건에 부합하지 X. 다만 확인 후 반복 중단)

line2: n-1

line3: n-1

line4: $\sum_{j=2}^nt_j$

line5: $\sum_{j=2}^n(t_j-1)$

line6: $\sum_{j=2}^n(t_j-1)$

line7: n-1

이 때 $t_j$는 j마다 while loop test 실행 횟수


## Running time
각 줄의 cost의 합 $T(n)$

$T(n) = c_1n + c_2(n-1) + c_3(n-1) + c_4\sum_{j=2}^nt_j + c_5\sum_{j=2}^n(t_j-1) + c_6\sum_{j=2}^n(t_j-1) + c_7(n-1)$

- $T(n)$의 best case   
:  A[1..n]이 이미 sorting이 된 경우. 모든 j(= 2,3, ... n) 에 대해 $t_j = 1 $

    $t_j = 1 $ 이므로, 

    $\sum_{j=2}^n(t_j-1) = 0$, $\sum_{j=2}^nt_j =n-1 $

    $T(n) = c_1n + c_2(n-1) + c_3(n-1) + c_4(n-1) + c_7(n-1)$   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $= (c_1 + c_2 + c_3 + c_4 + c_7)n - (c_2 + c_3 + c_4 + c_7)$

    $\rarr an + b$

    $\therefore$ best case는 n에 비례


- $T(n)$의 worst case   
: A[1..n]이 역순으로 정렬된 경우 $t_j = j $

    $\sum_{j=2}^n(t_j-1) = \frac {n(n+1)}{2} -1$, &nbsp;&nbsp;&nbsp; $\sum_{j=2}^nt_j = \frac{n(n-1)}{2} $ 이므로

    $T(n) = c_1n + c_2(n-1) + c_3(n-1) + c_4(\frac {n(n+1)}{2} -1) + c_5(\frac{n(n-1)}{2}) + c_6(\frac{n(n-1)}{2}) + c_7(n-1)$   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $= (\frac{c_4}{2} + \frac{c_5}{2} + \frac{c_6}{2})n^2 + (c_1 + c_2 + ... \frac{c_7}{2} + c_8)n -(c_2 + c_3 ...)$

    $\rarr an^2 + bn +c$

    $\therefore$ worst case는 $n^2$에 비례


- $T(n)$의 average case   
: $t_j = \frac{j}{2} $

    $\rarr n^2$에 비례   

leading term의 degree만 중요 ($\because$ rate of growth, order of growth에만 관심.)   
그리고 leading term의 degree는 $\theta$-notation으로 표기.   
$\therefore$ insertion sort의 worst-case의 running time은 $\theta(n^2)$


## Space consumption

입력으로 주어진 공간 외에 사용하지 않기 때문에,   
$\theta(n)$ space


## Insertion Sort의 특성
- 'inplace' (O) $\because$ n + c (c는 상수)

- 'stable' (O)

>stable하다는건,   
입력에 동일한 값 있는경우, 그들의 입력 순서 보존이 된다.


---

출처 : 2023-2 ITE2039 수업  
