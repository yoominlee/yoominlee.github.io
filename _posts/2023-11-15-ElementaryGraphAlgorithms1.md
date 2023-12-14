---
layout: post
title: Elementary Graph Algorithms part1:Graphs
subtitle: ITE2039 Algorithms and problem solving
categories: Algorithm
tags: [Algorithm, ITE2039]
use_math: true
---

Contents   
- Graphs(part1)
    - Graph basics
    - Graph representation
        - Adjacency-list representation
        - Adjacency-matrix representation
- Searching a graph (part2)
    - Breadth-first search
    - Depth-first search
- Applications of depth-first search(part3)
    -  Topological sort

---

## Elementary Graph Algorithms 1

### Graph basics

- Graph G는 V와 E의 쌍. (V,E)   
    (V: vertex, E: edge)
    - vertex는 아래 그림에서 원형인 node
    - edge는 아래 그림에서 선인 link

![1][1]

- Directed graph (= digraph)
    - 아래 파란색 edge는 **incident from** vertex 2,    
    **incident to** vertex 4
        - incident는 edge와 vertex 사이의 관계를 나타냄
    - 빨간색 edge는 self-loop
![2][2]

- Undirected graph
    - edge가 direction가지고 있지 않음
    - self loop 없음
    ![3][3]

- Adgacency (= 노드사이의 관계)
    - 만약 (u,v)가 edge라면, vertex v is adjacent to vertex u
    - undirected graph에서는 adjacency관계는 대칭(symmetric)
        - u is adjacent to v이면, v is adjacent to u
    - directed graph에서는, 대칭 관계가 아님! (❗주의)
        - 아래 그림에서, vertex 2 is adjacent to 1
        - 하지만 vertex 1 is not adjacent to 2
        ![2][2]
    
- Degree
    - vertex 2의 out-degree는 3
    - vertex 2의 in-degree는 2
    - degree = out-degree + in-degree
    ![2][2]

- Path 
    - 연속적인(consecutive) edge의 sequence
        - 여기서 주의할 점은 edge의 '순서'라는 것. 집합 아님!
        
        ![4][4]
    - 또한 path의 length는, path에 있는 edge의 수
        - 예를 들어, path <1,2,4,5>의 length는 3
    - vertex u에서 v까지 도달하는 path가 있다면, v는 u로부터 reachable 하다고 함.

- Simple path
    - path의 모든 vertices가 다르다면(distinct) 그 path는 simple하다고 함.
        - path <1,2,4,5>는 simple path
        - path <1,2,4,1,2>는 simple path가 아님     
        simple path되려면, 경로 안에 cycle포함 하면 안됨.

- Cycle and simple cycle
    - 만약 $v_0=v_k$라면, path $<v_0, v_1, v_2,..., v_k>$는 cycle
    - $v_1, v_2,..., v_k$가 distinct 하다면 cycle $<v_0, v_1, v_2,..., v_k>$는 simple
    - A path <1, 2, 4, 5, 4, 1>는 a cycle이지만 simple cycle은 아니다.
    - A path <1, 2, 4, 1>는 simple cycle
<br><br><br>
- An acyclic graph   
= cycle 없는 그래프

- A connected graph   
undirected graph가 connect 되어있다   
= 모든 pair의 노드가 path로 연결되어 있는 경우

- Connected components
    - undirected graph에서 최대로 연결된 vertex의 subset
<br><br><br>

- Strongly connected
    - 만약 vertex의 모든 pair가 서로서로 reachable 하다면 이때의 direct graph는 **strongly connected** 하다고 함

- Strongly connected components
    - Directly connected graph에서, 최대로(maximally) strongly connected 되어있는 (vertex의) subset
    ![6][6]
<br><br><br>

- A complete graph
    - 모든 pair의 vertex가 adjacent한 undirected graph
    ![5][5]

- A bipartite graph
    - G = (V,E)인 undiredted graph는 두 set $V_1, V_2$로 partition될 수 있고, 모든 edge는 양쪽에 걸침(=동일한 partition에는 edge 없음)
        - 그리고 위의 edge조건을 수식으로 표현 하면,   
            ```
            for each edge (u,v), either u∈V1 and v∈V2,or u∈V2 and v∈V1
            ```
        ![7][7]
<br><br><br>

- Forest
     - acyclic, undirected graph

- Tree
    - A connected forest
    - Tree의 조건: A connected, acyclic, undirected graph
    - Root, child 개념 X, 두 node 사이 연결 유무만 의미 O

    > 지금까지 본 tree는 direction 있었음   
    graph 의 일종으로써 tree는 일반적인 정의로 direction이 없는것. 특별한 경우로써 direction가지는 것 이야기 할것임.


![8][8]
>위 그림에서 좌측은 Tree,   
중앙은 Forest,   
우측은 cycle 있어서 tree X

> 정리하면, Forest는 tree의 집합   
Tree는 forest중에 connected 된 것

<br><br><br>


- Dag
    - <u>D</u>irected <u>a</u>cyclic <u>g</u>raph

![9][9]

> dag로 표현되는 응용 applicaion이 꽤 있음.   
    이런경우 dag의 특성 이용해 걔산 빠르게 하거나 approximation 하거나... 활용   
    graph 중 특별한 성질 가지는 것들이 tree, forest, directed acyclic graph 등.




- Handshaking lemma   
    if $G=(V,E)$가 undirected graph라면,   
    $\sum_{v∈V}degree(v)=2|E|$   
    -> degree와 edge의 개수 사이의 관계

- Tree: connected, acyclic, and undirected graph (좌측은 정의, 하단은 성질)
    - 어떠한 vertex도 **unique simple path**로 연결되어있다
        - unique하지 않다면, 반드시 cycle이 생김
    - 어떠한 edge라도 제거된 경우, graph는 **disconnected**된다. 
        - 특정 edge 지웠는데 그 양끝점 disconnect 되지 않고 연결되어 있다면, cycle이 있었다는 것. $\therefore$ 특정 edge 지우면 disconnect 됨.
    - 어떠한 edge라도 추가되는 경우, cycle을 포함하게 된다. 
        - 추가되는 그 양 끝점 연결하는 unique path가 있었을테니 cycle 생기게 됨.
    - |E| = |V| – 1 
    (node수는 edge수보다 항상 하나 작다)

    ![10][10]


- G is a tree.   
= G is a connected, acyclic, and undirected graph   
(초기 정의. 아래는 다른말로 표현한 같은 의미 가지는 말들)   
= In G, any two vertices are connected by a unique simple path.   
= G is connected, and if any edge is removed, the resulting graph is disconnected.   
= G is connected, |E| = |V| – 1.   
= G is acyclic, |E| = |V| – 1.    
= G is acyclic, but if any edge is added, the resulting graph contains a cycle.
> tree를 정의하는 여러가지 방법   
외울필요 없고, 이것 말고 위의 특성알아두면 됨.

```
✏️ 임의의 두 노드사이에서 unique한 simple path, edge수가 connectiveness 유지하는 최소한의 노드 (cycle 되지 않도록 하는 최대한) -> tree의 이 특성 잊지 말기
```

- The number of edges(일반적으로 edge와 node의 개수의 관계)
    - Directed graph:   
    $|E| ≤ |V|^2$   
    $\because$ self loop 까지 포함 하기에
    - Undirected graph:   
    |E| ≤ |V| (|V|–1) / 2   
    $\because$ self loop 불가하고, 서로 다른 두 node 사이에만 있을 수 있기에

### Graph representation
그래프의 표현 크게 두가지
- Adjacency-list representation
- Adjacency-matrix representation
#### Adjacency-list representation




#23








![11][11]

#### Adjacency-matrix representation







#### Adjacency-list representation, Adjacency-matrix representation 비교



---

[1]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/1.png
[2]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/2.png
[3]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/3.png
[4]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/4.png
[5]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/5.png
[6]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/6.png
[7]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/7.png
[8]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/8.png
[9]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/9.png
[10]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/10.png

[11]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/11.png
[12]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/12.png
[13]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/13.png
[14]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/14.png
[15]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/15.png
[16]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/16.png
[17]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/17.png
[18]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/18.png
[19]: /assets/images/post_img/2023-11-15-ElementaryGraphAlgorithms/19.png


출처 : 2023-2 ITE2039 수업  


