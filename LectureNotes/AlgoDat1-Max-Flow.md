Status: #LectureNote
Tags: [[Zettelkasten/Graph-Theory]]

# AlgoDat1-Max-Flow

### Important definitions for Flow networks
See [[Flow-Networks|Flow Networks basics]]

### What are the applications of Flow networks?
```ad-example
title:
Flow networks can be used to describe
- Oil pipes
- Traffic systems
- Computer Vision
...
```

### What are Residual Networks?
See [[Residual-Networks|Residual Networks]]

### What does weak duality mean?
This says that the value of the flow in a network with an s-t cut has to be less or equal to the capacity of the cut. See [[Weak-Duality|weak duality]]

```ad-note
title: 
If $|f| = c(S,T)$, then $f$ is a maximum flow and $(S,T)$ is a minimum cut.
```
### What is the Max-Flow Min-Cut theorem?

```ad-note
title:
If $f$ is a flow in a network $G$ then these statements are all equivalent:
1. there is an s-t cut with $c(S,T) = |f|$
2. $f$ is a maximum flow in $G$
3. $G_f$ (residual network) contains no augmenting paths
```

### What does strong duality mean?

```ad-note
title: 
If $|f^*| = c(S^*,T^*)$, then $f^*$ is a maximum flow and $(S^*,T^*)$ is a minimum cut.
```
```ad-question
title: What does the asterisk denote?
```

### What is the Ford Fulkerson Algorithm for? ^ford-fulkerson
This is an algorithm to calculate the maximum flow from a source to the sink in a flow network.

```ad-tip
title: Ford-Fulkerson Algorithm
![[Assets/img/ford_fulkerson.png]]
![[Assets/img/augment.png]]
```
If this algorithm terminates, then the residual graph doesn't contain any augmenting paths and the *computed flow is maximum*.

```ad-tip
title: Termination time Ford-Fulkerson
If $|f^*|$ is a maximum flow in the flow network $G$ and all capacities are *integral* (integers) then the algorithm terminates in $mathcal{O}(m\cdot |f^*|) \subseteq \mathcal{O}(mnC)$ time.
```
*C is the maximum edge capacity.*

```ad-caution
title: There are network where the Ford-Fulkerson algorithm doesn't terminate

```

### Are there better ways to choose augmenting paths?
```ad-example
title:
1. Look for paths with large residual capacity $\mathcal{O}(m^2 log C)$
2. Look for shortest paths (wrt. number of edges) $\rightarrow$ *Edmonds-Karp algorithm* $\mathcal{ O }(m^2 \cdot n)$
3. Look for all shortest paths before updating the flow and recomputing $G_f$ $\rightarrow$ blocking flows, *Dinitz algorithm* $\mathcal{ O }(n^2 \cdot m)$
```
*Here $m$ is the number of edges and $n$ the number of vertices.*

### What is maximum bipartite matching?

```ad-tip
title: matching
A *matching* is a subset $M$ of the set of edges in an undirected graph so that each vertex is the end of at most one edge in $M$
```
```ad-example
title: Matching example
![[Assets/img/matching.png]]
```

```ad-tip
title: bipartite
A graph is *bipartite* if it can be arranged in such a way that the end vertices for each edge are not in the same partition.
$$
    V = V_1 \sqcup V_2 \text{ and } E \subseteq V_1 \times V_2
$$
```
```ad-example
title: Bipartite graph example
![[Assets/img/bipartite.png]]
```

```ad-tip
title: Maximum bipartite matching
A matching in an undirected bipartite graph given by
$$
    G(V = V_1 \sqcup V_2, E \subseteq V_1 \times V_2)
$$
with the most possible elements (*maximum cardinality*)
```
```ad-example
title:  Maximum bipartite matching example
![[Assets/img/max_bipartite_matching.png]]
```

### How can we get maximum flow from maximum bipartite matching?

```ad-info
title:
**Given is an undirected bipartite graph then we:**
1. add a source and a sink node
2. add and edge from the source to every vertex in $V_1$ with capacity 1
3. add and edge with capacity 1 from every vertex in $V_2$ to the sink
4. give all original edges of the bipartite graph a direction from $V_1$ to $V_2$ and set their capacity to 1
```
```ad-example
title: Maximum Flow from maximum bipartite matching example
![[Assets/img/max-flow_bipartite-matching.png]]
```

### What is the cardinality of a matching in a flow network?

```ad-tip
title: 
An undirected, bipartite graph $G$ has a matching of cardinality k only if the corresponding flow network $G^′$ has a flow of size k.
```

### How can this be use for Image Segmentation?

```ad-question
title:
**We have a 2d image and want to separate the foreground and the background**
- the image can be represented by an undirected graph
    - the pixels are the vertices
    - and the pair of pixels $ij \in E$ are edges if they're next to eachother
```
```ad-info
title: Idea
We can give each pixel the likelihood *$a$ to be in the foreground* and *$b$ to be in the background*. Now we want to maximize
$$
    \sum_{i \in A} a(i) + \sum_{j \in B} b(j) - \sum_{\substack{ij \in E, \\ |\{i,j\} \cap A| = 1}} p(i,j)
$$
Maximizing the expression above is equivalent to minimizing
$$
    \sum_{i \in A} b(i) + \sum_{j \in B} a(j) + \sum_{\substack{ij \in E, \\ |\{i,j\} \cap A| = 1}} p(i,j)

$$
This would correspond to finding a *minimum s-t cut.*
```
Here $p$ is the *smoothness penalty* for the pixel pairs that is applied to the pixels if they lie in different partitions. *$A$ is the foreground partition.*

```ad-abstract
title: Method
**Transform undirected bipartite graph into a flow diagram:**
1. each undirected edge is replaced by a dummy vertex plus three directed edges. This is to avoid antiparallel edges.
    ![[Assets/img/image-seg_dummy-vertex.png]]
    ```ad-warning
    title: [[Zettelkasten/Flow-Networks#^simple-graphs|Simple graphs]] don't have antiparallel edges
    ```
2. Add a source node (foreground) with an *edge to every vertex $i$* and capacity $a(i)$
3. Add a sink node (background) with and *edge from every vertex $i$* and capacity $b(i)$

**Find the minimum s-t cut in this flow network**
![[Assets/img/image-seg_minimum_s-t_cut.png]]
```

### What is a flow circulation with demands?

```ad-tip
title: Demand
We have a no distinguished source and sink. Each vertex has a demand $d$ *(negative demand is supply)*. 
The flow conservation is modified to 
$$
    \sum_{u \in V} f(u, v) - \sum_{u \in V} f(v, u) = d(v)
$$
This must hold for all vertices in $V\textbackslash\{s,t\}$. The capacity remains unmodified.
```

```ad-example
title: Flow network with demads example
![[Assets/img/flow-network-demands.png]]
```

```ad-tip
title: Circulation
A circulation is a function $f$ that satisfies these contraints.
```

### How can we find the maximum flow from a circulation graph with demands?

```ad-note
title: How to transform a circulation graph into a flow network?
1. Add source and sink nodes
2. Add an edge from source to all vertices with negative demand  (supply) and set $c(s,v) = -d(v)$
3. Add and edge from each vertix with positive demand to the sink and set $c(v,t) = d(v)$
```

```ad-example
title: After transforming the circulation graph above we get the flow circulation
![[Assets/img/flow-network-demands-example.png]]
```

```ad-note
title:
A circulation network with the demands $d$ and the capacities $c$ has a circulation only if the corresponding flow network has a maximum flow with value
$$
    |f| = \sum_{v \in V:d(v) > 0} d(v) = \sum_{v \in V: d(v) < 0} -d(v)
$$
```

### How does adding lower bounds change the flow circulation network?

```ad-tip
title:
Introducing lower bounds $I(u,v)$ we have to change the capacity contraints such that
$$
    0 \leq I(u,v) \leq f(u,v) \leq c(u,v)
$$
holds for all $(u,v) \in V \times V$.
```
Then a circulation is a function that keeps these contraints.

```ad-example
title: Flow network with demands and lower bound example
![[Assets/img/flow-network-demands-lower-bound.png]]
```

### How can we simplify a flow circulation with demands and lower bounds to a flow circulation?

```ad-note
title:
In order to do this we
1. add the value of the lower bound ($I(u,v)$ to the vertix $u$
2. subtract the value of the lower bound of the vertix $v$
3. and reduce the capacity of the edge (u,v) by the value of the lower bound
```
```ad-example
title:
![[Assets/img/transformation_lower-bound_demand.png]]
```

```ad-info
title: 
A circulation network with demands and lower bounds has a circulation only if the corresponding flow network with transformed lower bounds has a circulation.
```
