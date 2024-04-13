Status: #LectureNote
Tags: [[Hamilton-Mechanics]] [[Topology]]

# ACP-MD-Hamilton-Mechanics

### Why do we need a better understanding of the mathematics in Hamilton Mechanics?
This helps with evaluating the [[Zettelkasten/Numerical-Integrators|numerical integrators]]

### What is the topology of phase space?
Usually phase space is a differentiable [[Zettelkasten/Mannifolds|mannifold]] that maps locally via a [[Zettelkasten/Local-Chart|local chart]] to [[Zettelkasten/Euklidean-Geometry|Euclidean space]].

If we use [[Zettelkasten/Periodic-Boundary-Conditions|PBC]] then the configuration space becomes a $3N$-dimensional torus.
If there are holonomic constraints (constraints that only rely on the coordinates) then the phase space is a submannifold of $\mathbb{R}^{6N}$. However because we assume to work within a local chart we can ignore mannifolds.
Additionally we express the system in degrees of freedom to make it possible to include holonomic constraints so for generalized coordinates and canonically conjungate momenta it will look like this
$$ 
    x \coloneqq (q_1,...,q_f,p_1,...,p_f)^T
$$
which is an element of $\mathbb{R}^{2f}$

### Prerequisites: Dynanmical systems and flow
**Solution of a system of first order DEQ:** a smooth function x(t) that satisfies
$$ 
    \frac{dx(t)}{dt} = X(x(t))
$$
this means that the change of the position with time should be equal to the trajectory determined by the vector field $X$. 

**Local flow:** 
A local flow which is determined by the vector field $X$ is a local one-parameter group of diffeomorphisms that 
- for fixed $x$ the function $\phi_t(x)$ is a solution of the flow equation $\Rightarrow$ because t is fixed we just look at the time evolution of x *(iterating through the mappings for each t and using the same x)*.
- for fixed $t$ the function $\phi_t(x)$ is a diffeomorphism (smooth and invertible) $\Rightarrow$ this follows from the definition for $\phi_t(x)$ because if t is fixed we just have a function that maps x to the position at time t.
- and that this holds: $\phi_s(\phi_t(x)) = \phi_{t+s}(x)$.

Also the flow satisfies the flow equation
$$
    \frac{d\phi_t(x)}{dt} = X(\phi_t(x))
$$

*Note:* A local one-parameter group of [[Zettelkasten/Diffeomorphisms|diffeomorphisms]] is a local map $(t,x) \mapsto \phi_t(x)$. This means that for each t there is a diffeomorphism that maps the positions from $U \subset \mathbb{R}^d$ to the positions at time t which will lie in in $\mathbb{R}$^d. So if $t=0$ then this is the identity map, which leave the positions x unchanged.


### What is symplecticity?
This is a linear mapping $A:\: \mathbb{R}^{2d} \rightarrow \mathbb{R}^{2d}$ that has following properties:
$$
\begin{aligned}
    A^T\mathbb{J}A = \mathbb{J}\\
    det(A) = 1
\end{aligned}
$$
where $\mathbb{J}$ is the symplectic normal form. From this follows that symplectic matrices are invertible and form a group (Sp(2d, $\mathbb{R}$)).
Furthermore symplectic transformations preserve the structure of Hamilton's equations. In classical systems such transformations are called canonical transformations.

Also a **differentiable map** is called **symplectic ** if the Jacobian $\partial \phi(x)$ is everywhere symplectic. This expression depends on the Jacobian because that is the derivative of a function in all directions and differentiable functions can be locally expressed as linear ones.
*More about symplecticity in script p.207-208*

### What is so special about hamitonian dynamical systems?
The vector field is fully determined by a scalar function (Hamilton function $\mathbb{R}^{2f} \rightarrow \mathbb{R}$) and $H(x)$ is differentiable twice.
The hamitonian vector field is defined by
$$
    X_H(x) \coloneqq \mathbb{J} \partial H(x).
$$
Multiplying with the symplectic normal form then swiches the positions of the gradients wrt $q_i$ and $p_i$ and the sign of the gradients wrt $q_i$. 
We can then write the hamitonian dynamical system as
$$
    \dot{x} = X_H(x)
$$

### What is the Liouville Operator?
[[Zettelkasten/Liouville-Operator|Liouville operator]] operator can be expressed by finding the time derivative of a phase space observable.
It is given by
$$
    i\mathcal{L} = \sum_j \dot{x_j}\partial_j
$$
By substituting in the Hamiltonian vector field in and evaluating the expression we can write the Liouville operator as the [[Zettelkasten/Poisson-Bracket|Poisson bracket]] of something (usually a phase space observable) and the Hamiltonian.
$$
    i\mathcal{L} = {\cdot, H\}
$$

### When are thy dynamics time-reversible?
When the trajectory followed in the reverse direction is also a solution of the EOM. So when flipping the signs of the momenta and reversing the time the EOM should't change the EOM.

### What are the Lyapunov exponents?
The Jacobian $J = \partial \phi_t(x)$ always transforms a sphere into a hyperellipse in $\mathbb{R}^{2f}$ by stretching it by some parameters $\sigma_1,...,\sigma_{2f}$ (which are non-negative) along orthogonal unit vectors $e_1,...,e_{2f}$.

In some systems some of these stretching factors grow exponentially with time
$$
    \sigma_i(t) = e^{\lambda_i t}
$$
for $t \rightarrow \infty.
These $\lambda_i$ are called **Lyapunov exponents** and can be calculated as
$$
    \lambda_i = \lim_{t \rightarrow \infty} \frac{ln \sigma_i(t)}{t}
$$

### What is a chaotic system of ODEs?
This is if the system produces very different outputs for very small changes in the initial conditions. In terms of the Lyapunov exponents a system is chaotic if $\lambda_i > 0$, Which is true for most systems in MD
