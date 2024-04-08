# Hamilton Mechanics

Hamilton mechanics serve the purpose of simplifying the system of second order differential equations from the [[Lagrange-Mechanics|Lagrangian]] to a system of 2n (n is the size of the system) first order differential equations. The Hamiltonian also has twice as many independent variables than the Lagrangian. This makes it possible to use much more transformations on the Hamiltonian that can be used to simplify the solution. In Hamiltonian mechanics we use the coordinates $q$ and $p$, which correspond to phase space.

The Hamiltonian is the [[Legendre-Transformation|Legendre transformation]] of the Lagrangian wrt. $\dot{q}$ and can be written as
$$ 
    H(q,p) = \sum_{\alpha} p_{\alpha}\dot{q}_{\alpha}(q,p) - \mathcal{L}(q, \dot{q}(q,p))
$$
where $p_{\alpha} = \frac{\partial L}{\partial \dot{q}_{\alpha}}$ are the generalized momenta and serve the purpose of an auxiliary variable mimicking the role of the first order derivatives $\dot{q}(t)$.

Then the EOM are given by
$$ 
\begin{aligned}
    \dot{q}_k = \frac{\partial H}{\partial p_k}\\
    \dot{p}_k = -\frac{\partial H}{\partial q_k}
\end{aligned}
$$

**How to:** 
1. Find Lagrangian
2. find $p_{\alpha}$
3. calculate Hamiltonian
4. derive EOM from Hamiltonian

With the [[Lagrange-Mechanics|generalized mass-weight]] tensor we can write the Hamiltonian as follows
$$ 
    H(q,p) = \frac{1}{2} q \cdot G^{-1}(q) \cdot q + U(q)
$$

In the case of Cartesian coordinates these EOM reduce to a similar system as the one postulated be [[Newton-Mechanics|Newton]].
