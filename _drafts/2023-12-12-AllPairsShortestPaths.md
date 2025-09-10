---
layout: post
title: All-pairs Shortest paths
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---

Contents   
- SSSP(single source shortest path) algorithm 사용하는 방법
- Floyd-Warshall algorithm
- Transitive closure of a directed graph

---

## All-pairs Shortest paths

```
✏️ Minimum Spanning Tree에서는 모든 노드를 연결하는 최소 cost인 tree 찾는것이 목표였고,   
이전에 본 Dijkstra는 single source 에 대해 shortest path.
이번 post에서는 임의의 두 node사이의 shortest path 찾는 all-pair shortest path를 찾는 방법 정리
```

### Using SSSP algorithms

- all-pairs shortest path 문제를 single-source shortest-path 알고리즘을 $|V|$회 실생해서 풀 수 있음.   
각 vertex들을 source로 반복해서 실행

- Nonnegative-weight edges -> Dijkstra's algorithm
    - Linear-array implementation   
    $O(V\cdot V^2) = O(V^3)$
    > array로 생각하면,   
    남은 것 중 d값 제일 작은 것 반복적으로 찾는것. $\therefore V^2$
    - Binary min-heap implementation   
    $O(V\cdot (VlgV+ElgV))=O(V^2\cdot lgV+VE\cdot lgV)$   
    $=O(VE\cdot lgV)$ $ \because V^2<VE$
    > min heap 쓰면,   
    각각의 node를 extract min 하는 시간 $VlgV$ + 각각의 노드에 대해 adjacent한 것들 Relax 적용. 이걸 decrease key로 구현. $lg V$ 최대 $E$번씩

- Negative-weight edges
    - Bellman-Ford algorithm   
    $O(V\cdot VE)=O(V^2E)$ / Dense graph라면 $O(V^4)$ ($\because $ edge많아서)
        >모든 edge relaxation 해야하므로 $VE$
    

```
✏️ All pair를 구하기 위해 single-source shortest path 알고리즘을 모든 노드(source로)에 대해 실행하는 방법은,
Simple 하지만 복잡도가 높다! 

따라서 all-pairs shortest path 문제를 푸는 다른 알고리즘인 Floyd-Warshall을 보려고 한다.
```

### Floyd-Warshall algorithm

#### Adjacency Matrix $W$
- $w_{i,j}=w(i,j)$

node $i$ 와 $j$ 사이 edge의 weight 표현

![1][1]


> 둘 사이의 edge 없는 것은 $\infin$   
두번째 행의 마지막 7은, 2번 노드에서 5번노드 가는 edge의 weight가 7임을 의미!

#### Shortest Distance Matrix $D$
- $d_{i,j}=\delta (i,j)$

임의의 두 node 사이의 shortest path 표현

![2][2]

> 각 셀의 값은 $\delta$ (delta)이고, 이는 길이를 의미.


#### Predecessor Matrix $\Pi$

- $\pi_{i,j}=NIL$ : $i=j$이거나 $i$에서 $j$까지 path 없는 경우
- $\pi_{i,j}$는 $i$에서 $j$로 가는 shortest path에서 $j$의 바로 직전노드(predecessor)

길이가 아닌 경로를 얻고싶은 경우 predecessor matrix

![3][3]

```
✏️ Dynamic programming 할때를 생각해보자! (경로 찾아가는것)
```

> diagonal은 self loop를 의미하기에 허용 X $\therefore NIL$

>EX. node 2 -> node 5 갈때 shortest path는?   
step1) $\Pi_{2,5}$ 위치를 보면, 1   
2 - - - - - 1 -> 5   
step2) $\Pi_{2,1}$ 위치를 보면, 4   
2 - - 4 -> 1 -> 5   
step3) $\Pi_{2,4}$ 위치를 보면, 2   
2 - 4 -> 1 -> 5   

$\Pi$ 를 가지고 $i$에서 $j$가는 경로 출력하는 알고리즘: 
```
PRINT-ALL-PAIRS-SHORTEST-PATH(Π, i, j)
    if i==j     // j부터 뒤에서 한자리씩 따라오다가 i와 같은 것 만난 경우 종료
        print i
    elseif πij == NIL
        print “no path from” i“to” j “exists”
    else PRINT-ALL-PAIRS-SHORTEST-PATH(Π, i, πij)   // i~Πij, j
        print j
```

### Floyd-Warshall algorithm

#### Intermediate Vertex
- simple path $p=<v_1,v_2,...,v_l>$에서 intermediate vertex는   
$p$의 $v_1$과 $v_l$ 사이에 있는 모든 vertex

#### Structure of a shortest path

- Floyd-Warshall 알고리즘을 한문장으로 정리하면,   
$i$에서 $j$로 갈때 intermediate vertex로 node $k$를 지나서 가는 경우와 아닌경우를 비교하며 작은 값으로 update   
$\therefore$ 기본 점화식은, $D_{ab}=D_{ak}+D_{kb}$


#### 동작 방식
- $V=\{1,2,...,n\}$이고,
- 어떤 vertex $i,j\in V$의 쌍



##### $D^0$ : 0번째 step   

![4][4]
$i$와 $j$사이에 연결 선 있다면 weight 입력, 
없다면 $\infin$

##### $D^1$ : 1번 노드를 intermediate vertex로

![5][5]

$d^{1}_{ij} = min(d^{0}_{ij}, d^{0}_{i1}+d^{0}_{1j})$   
1번 노드를 거쳐가는것과 거치지 않는 경로 두가지를 비교해 짧은 값으로 update

그리고 이때 predecessor를 기록하는 matrix인 $\Pi$도 아래와 같이 update
![6][6]


##### $D^2$ : 2번 노드를 intermediate vertex로

기존 길이와 2번 노드를 거쳐가는 경로의 길이를 비교!

![7][7]

distance update

![8][8]

predecessor update

##### 모든 노드에 대해 위와 같은 과정 반복


$\Pi^{(k)}_{ij}\begin{Bmatrix}\Pi^{(k-1)}_{ij} \;\; if\;\; d^{k-1}_{ij}\leq d^{k-1}_{ik}+d^{k-1}_{kj}\\ \Pi^{(k-1)}_{kj} \;\; if \;\; d^{k-1}_{ij}\leq d^{k-1}_{ik}+d^{k-1}_{kj} \end{Bmatrix}$
> 위 수식 중 윗줄은 기존 값이 k노드 지나는 경로값 보다 작아 update 되지 않는 경우   
아랫줄은 노드 k지나는 것이 더 작은 값으로 update 시키는 경우를 의미




##### Pseudo code
>$
FLOYD-WARSHALL(W)
$   
&nbsp;&nbsp;&nbsp;&nbsp;$n = W.rows$   
&nbsp;&nbsp;&nbsp;&nbsp;$D(0)=W$   
&nbsp;&nbsp;&nbsp;&nbsp;for $k = 1$ to $n$   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;let $D(k)=  (𝑑^{(k)}_{ij})$ be a new $n \times n$ matrix   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; for $i= 1$ to $n$   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for $j = 1$ to $n$   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $d^{(k)}_{ij} = min(d^{(k-1)}_{ij}, d^{(k-1)}_{ik}+d^{(k-1)}_{kj})$    
&nbsp;&nbsp;&nbsp;&nbsp;return $D(n)$


- Cost $\Theta(n^3)$


##### Cost 
: $O(V^3)$   
노드의 개수인 $n=|V|$이므로   
노드 횟수 $V$만큼 단계를 수행하고, 각 단계마다 $V^2$ 연산 수행.



```
✏️ 생각해 볼 point 1 : DP? Greedy?

Floyd-Warchall 알고리즘은 노드개수 N개 만큼 반복해서 점화식에 맞게 NxN matrix를 update 하기 때문에 DP. (DP는 sub problem으로 큰 problem을 푸는 것이라고 배웠었음)
Dijkstra가 Greedy
```

```
✏️ 생각해 볼 point 2 : DP라면 메모리는?

DP는 memory 문제가 있다. Floyd-Warshall이 DP라면 메모리는 얼마나 쓰는가?

D1 -> D2 -> ... -> Dn
D1을 가지고 D2를 만들고, D2를 가지고 D3을 만들고... 이를 반복하며 Dn을 만든다. 
다시말해서, Di로 Di+1을 만들고, Di+1로 Di+2를 만드는데 Di+2를 만들땐 Di가 필요 없다. 

따라서 어느순간 필요한 matrix는 2개.
-> 2n^2 => n^2
```



---

[1]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/1.png
[2]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/2.png
[3]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/3.png
[4]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/4.png
[5]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/5.png
[6]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/6.png
[7]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/7.png
[8]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/8.png
[9]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/9.png
[10]: /assets/images/post_img/2023-12-12-AllPairsShortestPaths/10.png


출처 : 2023-2 ITE2039 수업  


