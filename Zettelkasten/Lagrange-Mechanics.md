# Lagrange Mechanics

Lagrange mechanics are another way to describe the motions of particle systems (perhaps the most fundamental one), which get useful when describing a constraint particle system or having nontrivial symmetries for the potential energy (anything more than translational symmetry).
The Lagrangian for a particle system is given by
$$ 
    \mathcal{L} = K - U
$$
where $K$ and $U$ are the kinetic and potential energy. 
In [[Newton-Mechanics|Newton mechanics]] these are usually given in Cartesian coordinates. In Lagrangian mechanics generalized coordinates $q_{\alpha} = \{q_1,...,q_{3N}\}$ where
$$ 
    q_{\alpha} = q_{\alpha}(\textbf{r}^N)
$$
are used (these are functions of the Cartesian coordinates).
When used with Cartesian coordinates the formalism reduces to Newton's equation.
Generalized coordinates are any set of coordinates that describe the motion of a physical system (such as polar or spherical coordinates).

The full formalism for the Lagrangian EOM is given through the Euler-Lagrange equations:
$$ 
    \frac{d}{dt}\frac{\partial \mathcal{L}}{\partial \dot{q}_i} - \frac{\partial \mathcal{L}}{\partial q_i} = 0.
$$

**Constraints:** The constraints are functions of the coordinates that can only take on specific values.
$$ 
    \sigma_i(\textbf{r}^N) = c_i.
$$
A constraint restricts the system to a hypersurface. If there are more than one constraint, the system gets confined to the intersection of all hypersurfaces.

In generalized coordinates the kinetic energy takes the form of
$$ 
    K = \frac{1}{2} \sum_{i=1}^{N} m_i \dot{r}_i^2 = \frac{1}{2} \sum_{i=1}^N \sum_{\alpha, \beta = 1}^{3N} m_i \frac{\partial r_i}{\partial q_{\alpha}} \frac{\partial r_i}{\partial q_{\beta}}\dot{q}_{\alpha} \dot{q}_{\beta}
$$

Now we can define the mass-weighted metric tensor
$$ 
    G_{\alpha \beta}(q) = \sum_{i=1}^N m_i \frac{\partial r_i}{\partial q_{\alpha}} \frac{\partial r_i}{\partial q_{\beta}}
$$
which is symmetric ($G_{\alpha \beta}(q) = G_{\beta \alpha}(q)$) and write the Lagrangian in a vectorized way
$$ 
    \mathcal{L} = \frac{1}{2} \dot{q} \cdot G_{\alpha \beta}(q) \cdot{\dot{q}} - U(q).   
$$

The Lagrangian reduces the system to s = n - m (n independent generalized coordinates and m constraint forces) second order differential equations.
