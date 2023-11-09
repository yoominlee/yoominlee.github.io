---
layout: post
title: Amortized Analysis_Aggregation analysis (1/4)
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---

## Amortized Analysis
이전까지 operation의 asymptotic boundary 구했음. (e.g. sort 비교횟수-> boundary)   

이 chapter에서는, push-pop 할때 push와 pop 수행시간 각각 구해서 합하는게 아닌, push, pop 합해서 n번 발생했을 때 전체 cost 구하는 것.   

= 독립적으로 시간복잡도 구하는 것이 아닌, 여러 operation의 시퀀스 한꺼번에 시간복잡도 분석.

(최악의 경우를 과하게 잡지 않도록)

> 특정 일을 할 때 100번 진행하는 경우 99번 1분이 걸리고, 1번정도 10분이 걸린다. 이때 최악의 경우 10분으로 잡고 이 일을 반복하는 횟수를 곱하게 되면 너무 과하게 upper bound를 잡는다는 것에서 시작.   
각 시퀀스의 upper bound를 구하고 이를 진행 횟수만큼 곱하는 것이 아닌 한번 진행할 때에 대한 평균적 시간을 구해서 upper bound를 구하자.   
n회 진행 시 총 걸리는 시간 T(n)을 구할 수 있다면 T(n)/n이 한번 진행시 걸리는 시간이고, 이것이 한번 진행했을 때 최악의 시간(위 예시에서 10분) 보다 짧다면 평가절하를 줄인것.

> amortized 예시   
[참고](https://gazelle-and-cs.tistory.com/87)


Contents      

☑️ Aggregation analysis    
➖ Accounting method   
➖ Potential method   
➖ Dynamic Table


## Aggregation analysis
Amortized analysis의 수행시간 분석하는 첫번 째 방법

$T(n)$ : n회 연산에서 최악의 경우 걸리는 총시간    
(이때 n은 input크기 아니고 operation의 횟수)


최악의 경우에서, 한 operation의 평균 cost는 $T(n)/n$    
= amortized cost

amortized cost는 각 operation에서 동일함.

### 예시1: Stack operation 

- stack operation에는,
    - ```PUSH(S,x)```
    - ```POP(S)```
    - ```MULTIPOP(S,k)```

- ```PUSH```와 ```POP```은 $O(1)$시간 소요
    - constant

- operation을 n회 진행 시 실제 running time은 $\theta(n)$
    - operation n회의 총 cost는 n

- ```MULTIPOP(S,k)```
    - 실제 running time은 ```POP```이 실행된 횟수에 linear   
    ``` cpp
    MULTIPOP(S,k)
        while not STACK-EMPTY(S) and k>0
            POP(S)      // T(1)*k
            k = k-1
    ```
    > 위 코드의 while부분의 조건에 의해 아무것도 안하고 나올 수 O.   
    data가 k개 있다면 k회 pop. 

    $0\leq multipop \leq k$

    - ```MULTIPOP```의 cost는 $O(k)$

⭐   
그런데, ```PUSH```,  ```POP```, ```MULTIPOP```이 뒤섞여 n회 발생했다고 가정.(initial stack은 empty)    
```PUSH```,  ```POP```이 constant이고, ```MULTIPOP```은 k니까 $O(nk)$인가?   
-> X. 이상함.   
$\because$ data 없으면 mpop도 constant.    
(앞에서 push 없었다면 mpop도 constant: 둘이 dependent하다.)

#### Aggregate analysis
: 총 sequence n회의 upper bound를 구해서 더 tight한 bound 구할 수 있음.


- n개의 임의의 ```PUSH```,  ```POP```, ```MULTIPOP```이 섞인 operation이 주어지면,
    - $n \geq \#(push) \geq \#(pop)$   
    $2n \geq \#(push) + \#(pop)$ ⭐    
    - 따라서 total cost는 $O(n)$
    - Amortized cost는 $O(n)/n=O(1)$



### 예시2: Incrementing binary counter 

- k-bit의 이진수를 0부터 1씩 증가시키는 경우.

- array A[0..k-1] 사용   

    |A[k-1]|...|A\[1]|A[0]|
    |:---:|:---:|:---:|:---:|

- ```INCREMENT``` operation의 cost는 bit flip된 수에 비례.
    - bit가 0->1 혹은 1->0으로 바뀌는 경우 cost 있다고 한다.
    ```cpp
    INCREMENT(A)
        i = 0
        while i < A.length and A[i] ==1
            A[i] = 0    // bit flip, T(1)
            i = i + 1
        if i< A.length
            A[i] = 1    // bit flip, T(1)
    ```

> 위 코드 부가 설명    
while문에서는, binary counter의 가장 낮은 자리에서 시작해서 처음으로 0 만날때 까지 1을 0으로 바꾸는 작업.   
if문 부분은, 현재 index위치의 값을 1로 변경. (bit flip)

![1][1]

그런데 ```INCREMENT```의 single execution은 (모든 비트1인) worst case에서 $\theta(k)$ 시간 소요되고,    
initially zero counter는 최악의 경우 n회 ```INCREMENT```에 $O(nk)$시간 소요

#### Aggregate analysis
: n회의 ```INCREMENT```에서 매번 bit flip이 모든 비트에서 일어나는 것이 아니기 때문에 더 tight한 bound 만들 수 있음.

![2][2]

위의 경우,    
A[0]자리의 bit flip 하는 경우 : $n= n/2^0$   
A\[1]자리의 bit flip 하는 경우 : $n/2= n/2^1$   
A\[2]자리의 bit flip 하는 경우 : $n/4 = n/2^2$   
A\[3]자리의 bit flip 하는 경우 : $n/8 = n/2^3$   

-> 총 sequence에서 flip하는 횟수⭐ :   
$\sum_{i=0}^{k-1} \lfloor n/2^i\rfloor < \sum_{i=0}^\infin n/2^i =2n$   
$\therefore total cost = O(n)$

Amortized cost = $O(n)/n = O(1)$


### Running time
$O(n)$ time in total

### Amortized cost
$O(n)/n=O(1)$ 


---

[1]: /assets/images/post_img/2023-11-07-AmortizedAnalysis/1.png
[2]: /assets/images/post_img/2023-11-07-AmortizedAnalysis/2.png

출처 : 2023-2 ITE2039 수업  
