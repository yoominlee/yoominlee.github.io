---
layout: post
title: Single-Source Shortest Path
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---

Contents   
- Definition
- Dijkstra's algorithm
- The Bellman-Ford algorithm
- Single-sorce shortest paths in directed acrylic graphs

---

## Single-Source Shortest Path

```
✏️ 이전 Minimum Spanning Tree에서는 모든 노드를 연결하는 최소 cost인 tree 찾는것이 목표였음.
```

이번 post에서는 전체 tree가 아닌 path 찾는것이 목표.

### Definition 
사용하는 개념들 정리

#### Edge weight 
: 특정 edge의 가중치

#### Path weight 
: Path에 있는 모든 edge weight들의 합


#### Shortest path
u에서 v로 가는 path 중 weight가 최소인 것
(이때 u는 source, v는 destination)

#### Shortest path weight
u에서 v까지 가는 shortest-path의 weight로, $\delta(u,v)$라고 표기


#### Shortest path problem
Shortest path문제는, source와 destination의 개수에 따라 4종류가 있다   

- Singles-source & Single destination

- <u>**Single-source (& all destinations)**</u>

- Single-destination (& all sources)

- All pairs


single source (& all destinaton) 문제로 다른 모든 문제 풀 수 있기에


#### Negative-weight edges
>생각해볼 point   
모든 negative-weight edge들이 문제를 유발하는가?   
모든 negative-weight cycle이 문제를 유발하는가?   
모든 reachable negative cycle이 문제를 유발하는가?   

$\Rarr$ source에서 reachable 한 negative-weight cycle이 없을 때 single-source shortest path가 정의 될 수 있다

#### Cycle
shortest path는 cycle을 포함하지 않으므로,   
$\therefore$ shortest path는 최대 $|V|-1$

#### Predecessor subgraph 

모든 SSSSP들을 compact하게 저장하는 shortest path tree

optimal substructure 


> 푸는과정에서 shortest path 기록하며 update,   
최종적으로 predecessor subgraph


#### Relaxation 


```
RELAX(u, v, w)
    if d[v] > d[u] + w[u, v]
        then d[v] ← d[u] + w[u, v]
            π[v]← u
```

### Dijkstra's algorithm

모든 weight nonnegative일때 정상작동

> 동작방식   
1) 해당 노드로부터 갈 수 있는 노드들의 cost 갱신 (다이나믹 프로그래밍)
2) 방문 안한 노드 중 가장 cost 작은 노드 선택 (Greedy 알고리즘)
3) 1,2 반복

```
DIJKSTRA(G, w, s)
    INITIALIZE-SINGLE-SOURCE(G, s)  // 첫노드 0, 나머지 ∞
    S = Ø   // empty set
    Q = G.V
    while Q ≠ Ø
        u = EXTRACT-MIN(Q)  // S 시작 노드 1개에서 시작해서, 
                            // Q에 남아있는 것 중 d값 제일 작은 것 
        S = S ∪ {u}
        for each vertex v ∈ G.Adj[u]
            RELAX(u, v, w)
```

> Negative-weight 없다는 가정하에 동작   
이런 제한 있음에도 실제 application 또한 negative 많지 않기에 유용

> shortest path가 알려진 것들의 집합 S, shortest path 모르는 것들은 V-S에.   
Dijkstra의 목표는 모두 S에 넣는 것.


#### Running time
while loop 이전까지 $\rarr |V|$   

while loop 내부는    
```EXTRACT-MIN(Q)``` : $O(|V| \cdot lg|V|)$   
```RELAX(u,v,w)``` : $O(|E|\cdot lg|V|)$

- (unsorted) array 사용한 경우, $O(V^2)$
    > 매번 제일 작은 것 찾는 시간이 n에 비례.   
    $\therefore n^2$
- heap 사용하면, $O(VlgV+ElgV)$


#### 증명

##### 증명에 사용할 Definition 

u에서 v까지 distance   
= $\delta (u,v)$ = 최단 거리


##### Problem

NONNegative인 edge weight를 가진 Directed graph $G(V,E)$와    
Special source vertex $s \in V$ 가 주어졌을 때,   
Source vertex에서 $G$의 모든 vertex까지 distance를 구하라

- $d[v]$ : estimates the shortest path = 지금까지 추정하는 최단거리
- $\pi[v]$ : predecessor pointer of the path = u에서 v까지 가는 path인 경우 v 바로 앞 노드(=predecessor)

##### Principle observation

- Short path의 모든 subpath 또한 항상 shortest path여야한다.   
    > 각 vertex에 대한 shortest path의 추정을 $d[v]$에 저장(유지)해둔다
- 초기에는, $d[s]=0$, $d[v]=\infin$
- $d[v]\geq \delta(s,v)$ : 알고리즘이 진행되면서 $d[v]$가 $\delta(s,v)$에 수렴할 때 까지 update 진행   
(이 process를 relaxation이라고 한다. = relaxation 통해 $d[v]$ 업데이트)

```
if(d[u]+ w[u, v]< d[v])
    d[v]= d[u]+ w[u, v];
    π[v]= u;
```

##### 진행

- vertex들의 subset $S ( \subseteq V)$ 를, shortest distance를 '안다'고 주장하는, $d[v] = \delta(s,v)$로 유지   
= $d[v] = \delta(s,v)$인 것들을 $S$에 넣어줌

- 초기에 $S=\{ \}$. 그리고 각 stage 마다 하나씩 vertex들을 $V-S$에서 선택함

- $d[u]$가 최소인 vertex를 선택. 그리고 이를 모든 operation(Insert, Delete_min, Decrease_key)이 $O(lgn)$시간에 수행 될 수 있도록 priority queue로 구현

- 각 stage 마다 
    - unknown vertex 중 최소의 $d[v]$값을 가지는 vertex $u$ 선택
    - $s$에서 $u$로 가는 shortest path는 안다고(known) 정의
    - update $d[v]$ : $d[v]$가 개선되었다면 $d[v]=d[v]+w[u,v]$로 update    
    ($v$로 가는 path에 $u$를 사용하는 것이 좋은 아이디어인지 결정)


##### Lemma (보조정리)
vertex $u$가 $S$에 추가되었을 때, $d[u]=\delta (s,u)$

##### Proof
>증명하고자 하는건,    
"Node $u$의 $d$값이 제일 작아 (extract-min 통해서)선택되면,
$u$의 $d$값은 실제 $\delta$(delta)이다"

"Proof by contradiction" 사용

>(모든 weight가 STRICTLY positive라고 가정)

vertex $u$가 $S$에 추가되었지만 $d[v]\neq \delta(s,v)$라면,    
$d[v]> \delta(s,v)$ ($\because$ $d$는 $\delta$보다 크거나 같다는 정의)

$u$를 추가하기 직전 상황을 검토해 보면,   

$s$에서 $u$까지 실제 최단거리를 $s\rarr x\rarr y\rarr u $ $(x\in S, y\in V-S)$라고 하면,    
> $d[v]\neq \delta(s,v)$라고 했기에 최단거리는 따로 있는 것.

그리고 $s$에서 $u$까지 path의 중간에 $y$가 있고, 모든 edge는 positive여서 $\delta (s,y)<\delta (s,u)$성립

$s\rarr x\rarr y\rarr u $가 최단경로라 가정했기에,   
$d[y]=\delta(s,y)<\delta(s,u)<d[u]$ 

$\therefore u$ 이전에 $y$가 추가되었어야 함. $\rarr$ contradiction to our assumption

📌 $y=u$일 수 없는가? $\rarr$ NO!   
$\because d[v] = \delta(s,v)$ 이고, 우리는 $x$를 추가하기 전에 relaxation 을 적용했기 때문




#### Bellman-Ford algorithm
: single source shortest-path problem을 negative weight도 포함하는 general case에 대해 푼다. 


```
BELLMAN-FORD(G, w, s)
    INITIALIZE-SINGLE-SOURCE(G, s)
    for i= 1 to |G.V| -1 // 모든 shortest path의 길이 구하는 loop
        for each edge(u, v) ∈ G.E // n-1번째 node까지 순차적으로 RELAX
            RELAX(u, v, w)
    for each edge(u, v) ∈ G.E // negative weight cycle 있는지 검사하는 loop
        if v.d > u.d + w(u, v) // negative cycle이 있다는 뜻
            return FALSE
    return TRUE
```
> 모든 shortest path의 길이 구하는 부분에서 n-1인 이유   
n-1 : 모든 node.   
$\therefore$ n-1보다 크면 중복 발생한다는 것   
= cycle 有






#84









```
❗ Prim VS Dijkstra
동작 아이디어가 유사해서 헷갈려서 정리해 본 두 알고리즘의 차이점

<목표 차이>
Prim : Minimum Spanning Tree
- Undirected weighted graph에서, 모든 node연결이 목표
-> 집합 S과의 최소 distance인 node 찾음

Dijkstra : Shortesst Path
- nonnegative weight의 graph에서 두 node 잇는 shortest path 찾는 것이 목표
-> 집합 S의 시작 node와의 최소 distance 찾음

위와 같이 두 알고리즘의 목표가 다르다는 차이 뿐 아니라 

<동작 조건 차이>
Prim은 undirected 에서만 동작, Dijkstra는 무관
Prim은 negative weight 가능, Dijkstra는 negative 불가능
```



---

[1]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/1.png
[2]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/2.png
[3]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/3.png
[4]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/4.png
[5]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/5.png
[6]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/6.png
[7]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/7.png
[8]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/8.png
[9]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/9.png
[10]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/10.png

[11]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/11.png
[12]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/12.png
[13]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/13.png
[14]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/14.png
[15]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/15.jpg
[16]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/16.png
[17]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/17.png
[18]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/18.png
[19]: /assets/images/post_img/2023-12-11-Single-SourceShortestPath/19.png


출처 : 2023-2 ITE2039 수업  


