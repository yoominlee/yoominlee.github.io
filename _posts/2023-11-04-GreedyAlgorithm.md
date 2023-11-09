---
layout: post
title: Greedy Algorithms
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---


Contents   
- Introduction 
- An activity selection problem
- Elements of the greedy strategy
- Huffman codes


---

## Greedy Algorithms
그 순간순간 가장 좋다고 생각하는 결정을 내리는 알고리즘

locally optimal이 global optimal solution으로 이끌 것이라는 희망을 가지고 선택


❓subproblem이 해결되기 전에 결정 내림


### An activity selection problem

다양한 activity들이 있을 때 가장 많은 수의 activity 넣기

- 한개의 강의실에 n개의  lecture있다
- 수업 수 최대로 고른다

위 두개 가정.

![1][1]

activity의 set $S =\{a_1,a_2, ..., a_n\}$

activity $a_i$ 의 시작시간은 $s_i$, 끝나는 시간은 $f_i$   
$0 \leq s_i < f_i < \infin$   
activity  $a_i$와 $a_j$의 진행 시간인 $[s_i,f_i)$와 $[s_j,f_j)$가 겹치지 않는다면 둘은 compatible 하다고 함. 

이때 가능한 최적 해:   
![2][2]

![3][3]

largest subset은 여러 경우의 수 나올 수 있음.

#### Optimal substructure

![4][4]

종료시간이 가장 빠른 것 반복적으로 선택

종료시간에 따라 sort 한 경우, 가장 빨리 끝나는 활동 선택하고, 그 활동이 끝나는 시간을 기준으로 가장 빠른 활동 하는 것 반복

#### 증명 방법

"가장 먼저 끝나는 activity가 어떤 optimal solution이던 들어간다"를 증명하면 됨.

-> proof by contradiction   
: 제일 먼저 끝나는 것 제외하고 optimal solution 선택한 경우에도, 이를 제일 먼저 끝나는 활동으로 대체 가능하다


### Elements of the greedy strategy
❓
- Greedy-choice property      
    - subproblem이 solve되기 전에 결정 내림(make choice)   
    - 오직 하나의 subproblem이 생성됨

- Dynamic programming
    - subproblem이 solve된 후에 결정 내림   
    - 몇몇의 subproblem이 생성될 수 있음   
    (subproblem의 최적해를 기록해두고 더 큰 문제 풀고자 함)

#### Greedy vs Dynamic programming


- knapsack 문제
    - n개의 item 있고, i번째 item은 $v_i$의 가치(가격)와 $w_i$의 무게를 가진다.   
    - 최대 $W$의 무게를 담을 수 있을 때 최대로 담는 경우 구하기 

![5][5]

<물건을 쪼갤 수 있는 경우>
- Fractional knapsack => Greedy algorithm
    - per 무게마다 가장 가치가 높은 item 선택
    - item별로 각 단위무게(pound)마다 가치 계산 $v_i/w_i$



<물건을 쪼갤 수 없는 경우>
- 0-1 knapsack => Dynamic programming


a) 에 보이는 item을 knapsack에 넣는 문제일 때    
b) 0-1 knapsack 문제. (1,2 담으면 3 담을 수 없음)      
c) fractional knapsack문제


### Huffman codes
: 데이터 압축(compress) 시 많이 사용하는 technique   
효율적인 데이터 압축법

#### 등장 빈도수에 따른 길이 반영 비교

- 3-bit의 고정길이(fixed length) 코드
![6][6]
=> 총 300,000 bits


- variable-length code 
![7][7]
=> 총 224,000 bits   
(45·1+13·3+12·3+16·3+9·4+5·4)·1000

> 많이 등장하는건 짧은 비트로, 적게 등장하는건 긴 비트로 -> compressing


#### 가변길이(variable-length) 코드의 encoding and decoding 
a:0, b:01, c:1로 encode 한 경우,   
001을 decode시, aac로도, ab로도 해석할 수 있게 되는 문제 발생.

#### Prefix codes
>prefix = 접두어

특정 문자가 다른 문자의 접두어가 안되는 특징 가진 코드 -> 유일하게 decoding 가능해져야 함

예시 1)
![8][8]
>모든 노드가 leaf이거나 children이 2개인 full binary tree

예시 2)

![9][9]
>3-bit fixed-length code도 prefix code이다.

#### Tree T의 cost
위와 같이 binary tree 사용해 (겹치지 않게 decoding되는)prefix code로 만들 수 있는데, 이 때 cost 최소화 하는 법을 생각해보면,   

$f(c)$ : character c의 빈도수   
$d_T(c)$ : c의 codeword 길이 (= tree에서 c의 depth)   
라고 하면,    
$B(T)=\sum_{c\in C}f(c)d_T(c)$

=> 위 식에 의하여 빈도수가 높은 문자는 길이가 짧아야(root에 가까워야) 하고, 빈도수가 낮은 경우 길이가 길도록(root에서 멀도록)한다.   
optimal : <u>Full binary tree</u>

#### Huffman code
> Huffman이 Huffman code라고 불리는 optimal prefix code를 구성하는 greedy 알고리즘을 고안

##### 트리 만드는 단계

1. 문자들을 빈도수에 따라 오름차순으로 정렬한다
![10][10]

2. 가장 빈도수 적은 두 노드를 선택해 트리로 구성 (좌측이 빈도수 더 적게)
![11][11]
이 때 node에 둘의 frequency 합친 빈도수로 가상의 character 생성

3. 이미 선택된 문자 제외하고 가상의 문자 포함 한 문자들 중에 빈도수 가장 작은 2개 선택 후 트리로 구성
![12][12]   
![13][13]
    >이 예시의 경우 이전단계에서 선택한 것이 다른(c와 b) 문자에 비해 빈도수가 높아서 선택되지 않은 것 뿐.   
g의 빈도수(f화 g의 합)가 10이었다면 선택 되었을 것임.

4. 더이상 노드 없을 때 까지 반복
![14][14]
![15][15]
    > 위 단계 마친 후 가상의 문자(g,h) 2개와 실제 문자(d,a) 2개 총 4개에서 빈도 수 비교. 14,16인 문자 두개 선택됨.   
5. 반복 & 최종
![16][16]

=> 가장 frequency 낮은 2개 묶어서 그걸 대료하는 가상의 character 뽑고,   
그것까지 포함한 frequency 비교

> ✏️ 최종 tree의 형태가 어떻게 정해진 것인지 헷갈렸었는데,   
<u>특정 모양이 정해진 것이 아니라 어디서 어떻게 묶이는지는 **frequency**에 의해 결정.</u>   
가상의 node 또한 frequency 할당되기에 뭐가 먼저 묶여 어떤것과 대등하게 될지는 frequency에 의해 형태 결정됨.   
(예를 들어, 빈도수 가장 작은 두개를 합한 빈도수가 계속해서 나머지 문자들의 빈도수보다 작을 경우, 한쪽으로 쏠린 형태의 tree)

##### Min Heap
: 가장 바람직한 자료구조

> heap은 array형태로 구성

![18][18]

위 문자의 빈도수로 min heap tree구성
![19][19]

맨 위의 노드 뽑은 뒤 가장 마지막노드를 위로
![20][20]

min heapify 진행 후 다시 맨 위 노드 추출
![21][21]

max heapify 진행하는것은 동일하지만, 추출한 두 노드의 frequency의 합으로 가상의 노드를 생성 후 min-heap의 맨 뒤에 넣고 다시 min heapify 진행
![22][22]

맨 위 노드 뽑고 다시 min heapify 2번 반복
![23][23]

가상의 노드 tree에 추가 후 min heapify
![24][24]

가상의 노드가 선택된 것
![25][25]

반복...
![26][26]

![27][27]

![28][28]

![29][29]


최종
![30][30]

#### Running time

min heap 만드는데 : $O(n)$   
delete min 2회, insert 1회 : $O(nlgn)$   

>$\because$ delete min의 경우, root에서 최악의 경우 leaf 까지 내려와야함   
insert도 마찬가지. 

=> $O(nlgn)$   
>$nlgn$을 upper bound로 가짐


#### Proof 1
[Lemma 16.2]

- 빈도수는 $f[c]$, 각 문자 $c$는 $c\in C$
- $x,y$는 $C$에 포함되는 가작 적은 빈도수를 가지는 두 문자.
- $x,y$는 동일한 길이의 마지막bit만 다른 codeword를 가지고 있을 때 (즉 parent공유) 가정.

임의의 optimal prefix code tree T를 설정.   
(아래 그림의 좌측 tree. x와 y가 가장 아래 level에 있지 않음.)
![31][31]

이 때 다른 optimal을 나타내도록 x와 y를 maximum 깊이로 옮긴 두가지 경우가 우측 두 tree $T', T''$
<br/> <br/> <br/> 
$T$--(x, a교체)-->$T'$--(b,y교체)-->$T''$
<br/> <br/> <br/> 
"$T$가 optimal이면 $T''$ 이 optimal이다"를 증명하고자함.    
= "$T$가 optimal이면 $T''$ 이 optimal이 아님"이 거짓임을 보이기 (proof by contradiction)
 <br/> <br/> <br/> 

$T$가 optimal일때 $T'$ 이 optimal이 아니려면,

$B(T)-B(T')$이 음수여야 함.
이를 조금 더 풀면,

$B(T)-B(T') $   
$= ( f(x) \cdot d_1 + f(a) \cdot d_2 )-( f(x) \cdot d_2 + f(a) \cdot d_1 )$   
$=(d_1-d_2)(f(x)-f(a))$

이때 $(f(x)-f(a))$가 음수임을 이미 알고있기 때문에 $(d_1-d_2)$가 양수여야 하는데 $d_1>d_2$ 불가능.


#### Proof 2
[Lemma 16.3]








































```cpp
PRINT-STATIONS(l,l*,n)
    i = l*
    print "line"i",station"n // 여기까진 constant
    for j=n down to 2 // n에 비례
        i = l[i][j]
        print "line"i",station"j-1
```


=> $2^n$ 걸리는 것을 $\theta(n)$으로 해결 가능

||Space|Time|
|:---:|:---:|:---:|
|Assembly-line scheduling|$\theta(n)$|$\theta(n)$|
|Rod cutting|||
|Longest common subsequence|||
|Matrix-chain multiplication|||



---

[1]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/1.png
[2]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/2.png
[3]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/3.png
[4]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/4.png
[5]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/5.png
[6]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/6.png
[7]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/7.png
[8]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/8.png
[9]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/9.png

[10]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/10.png
[11]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/11.png
[12]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/12.png
[13]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/13.png
[14]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/14.png
[15]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/15.png
[16]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/16.png
[17]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/17.png
[18]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/18.png
[19]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/19.png

[20]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/20.png
[21]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/21.png
[22]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/22.png
[23]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/23.png
[24]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/24.png
[25]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/25.png
[26]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/26.png
[27]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/27.png
[28]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/28.png
[29]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/29.png


[30]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/30.png
[31]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/31.png
[32]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/32.png
[33]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/33.png
[34]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/34.png
[35]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/35.png
[36]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/36.png
[37]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/37.png
[38]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/38.png
[39]: /assets/images/post_img/2023-11-04-GreedyAlgorithm/39.png

출처 : 2023-2 ITE2039 수업  
