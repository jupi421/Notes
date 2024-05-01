Status: #Definition
Tags: [[Zettelkasten/Graph-Theory]] [[Flow-Networks]]

# Residual Networks

### Definition: Residual Network
A residual network $G_f$ is given by the union set of the edges with flow $f < c(e)$ and the reverse edges with flow $f > 0$, ie. the edges that have some residual capacity that can be utilized into the other direction.
```ad-example
title: Flow network and corresponding residual network
![[assets/residual_graph.png]]
```
```ad-tip
title: Set of Edges in a residual network
$$
    E_f = \{e | e \in  E \land f(e) < c(e)\} \cup \{e^{rev} | e \in E \land f(e) > 0\}
$$
```
```ad-tip
title: Capacity of the residual network
$$
c_f(e) =
\begin{cases}
    c(e) - f(e) & \text{if $e \in E$}\\
    f(e^{rev}) & \text{if $e^{rev} \in E$}
\end{cases}
$$
```
Where the first part is the *remainig capacity* and the second part is the *cancellable flow* capacity.

### Definition: Augmenting Path

This is a simple path in the residual network. The flow $f_P$ then follows this path.
```ad-example
title: Flow along an augmenting path example
![[assets/augmenting_path.png]]
```
The residual capacity is called the *bottleneck capacity* of an augmenting path is the smallest capacity along an edge along that path.

```ad-tip
title: Flow along an augmenting path
$f_P: V \times V \rightarrow \mathbb{R}$ where 
$$
    f_P(u,v) = 
\begin{cases}
    c_f(P) & \text{if $(u,v)$ is on P}\\
    0 & \text{otherwise}
\end{cases}
$$
```
This means that the flow can only be along that augmenting path.

```ad-info
title: Lemma Augmenting Paths
If $f$ is a flow in a flow network $G$ and $f_P$ is the flow along an augmenting path we can write the sum of these flows as
$$
    (f + f_P)(u,v) = 
\begin{cases}
    f(u,v) + f_P(u,v) - f_P(v,u) & \text{if $(u,v) \in E$}\\
    0 & \text{otherwise}
\end{cases}
$$
is also a flow in the network $G$ with the value $|f + f_P | = |f| + |f_P|$
```
