Status: #Definition:
Tags: [[Zettelkasten/Graph-Theory]]

# Flow-Networks

### Definition: Flow Network

Flow Networks are directed, weighted and simple Graphs  with a souce and sink node. ^simple-graphs

```ad-note
title: Simple graph  
Simple graphs have no pairs of antiparallel edges or loops. 
```
```ad-tip
title: Flow Network
$$
    G(V, E, c, s, t)
$$
V: *is the set of vertices (nodes)*
E: *is the set of edges*
$c(e)$: *is the capacity of an edge $e \in E$ and is $\geq 0$*
s: *is the source*
t: *is the sink*
``` 

if $(u,v) \notin E$ then the capacity $c(u,v) = 0$.

```ad-example
title: Flow Network example
![[assets/flow_network.png]]
```
### Definition: Flow

The flow is a function $f: V \times V \rightarrow \mathbb{R}$ with the properties

```ad-tip
title:
1. the flow has to be between 0 and the capacity of the edge for all edges $(u,v) \in V \times V$ (*capacity constraint*)
2. The total flow going out of a vertice has to be equal to the total flow going in (*flow conservation*)
```
```ad-tip
title: Value of the flow $|f|$ 
$$
    |f| = \sum_{v\in V} f(s,v) - \sum_{v \in V} f(v,s) \geq 0
$$
```
Which means that the value of the flow is the difference of everything that goes out of a vertice and everything that goes in.

### Definition: s-t cut

An s-t cut divides the flow network so that the source lies in one part and the sink in the other one.

```ad-tip
title: Set of edges that form the cut 
$$
    E(S,T) = \{(u,v) \in E | u \in S \land v \in T \} = E \cap (S \times T)
$$
where $E$ is the set of all edges.
```


```ad-tip
title: Capacity of the cut
$$
    c(S,T) = \sum_{u \in S, v \in T} c(u,v) \equiv \sum_{e \in E(S,T)} c(E)
$$
```
This means that we add the capacity of all edges that go from S into T.

```ad-example
title: Example of an s-t cut
![[assets/s-t_cut.png]]
The capacity of this s-t cut is $c(S,T) = 18$
```

```ad-note
title: Minimum s-t cut
The minimum s-t cut is the s-t cut with the smallest capacity
```

### Lemma Flow Value

```ad-info
title: Lemma: Flow Value
If $f$ is a flow in a network $G$ and there is an s-t cut, then the value of $f$is equal to the net flow across the cut.
```
