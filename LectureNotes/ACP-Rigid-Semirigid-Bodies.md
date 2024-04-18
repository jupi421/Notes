Status: #LectureNote
Tags:

# ACP-Rigid-Semirigid-Bodies

### What is the time scale problem in MD?
This is the fact that we should pick $\Delta t$ smaller than the time scale of the fastest motion in the system. If we have a system of molecules then the bonds in the molecules would be vibrating. So to carry out a MD simulation we'd have to have a time step shorter than these vibrations which would mean that we'd have to calculate the forces much more often and this can be expensive.

### Why do we consider the bonds as rigid instead of vibrating?
In doing so we deal with the time scale problem of having fast bond vibrations compared to the molecular motion in the system. Because these vibrations are so fast, 
$$
    \hbar \omega \gg k_BT
$$
it means that they're essentially frozen in their ground state which in the classical approximation corresponds to rigid bonds. The vibrations in a water molecule would occur at a temperature of 5300K.

### What effect does introducing constraints have on the average?
They would introduce an artificial bias. This is because in soft but hard constraints all degrees of freedom are included in the momentum integral, whereas for hard constraints some degrees of freedom are eliminated and then we have a deviation from the original value by some factor. This bias can be calculated by comparing the probability distribution for the generalized coordinates with hard constraints $\rho^H$ with the probability distribution for the generalized coordinates with soft but stiff constraints and we get
$$
    \frac{\rho(c,q^S)}{\rho^H(q^S)} = \frac{C}{A}\sqrt{\frac{det(G(c,q^S))}{det(G_{SS}(q^S))}}.
$$
This is the bias we have to account for when doing MD simulations with rigid constraints. It was found out that this ratio is the determinant
$$
    \frac{det(G(c,q^S))}{det(G_{SS}(q^S))} = det B(q^S)
$$
where $B$ is an $n\times n$ matrix that depends only on the derivatives of the n constraints compared to the mass-weighted metric tensor that has the $3n$ coordinate derivatives. Using this we can simplify the bias correction to
$$
    \rho(c,q^S) \propto \frac{\rho^H(q^S)}{\sqrt{detB(q^S)}}.
$$

### How is a molecule represented in MD?
In the case of the system having $N$ particles and each molecule consists of $n$ particles with mass $m$ we can write the total force on particle $i$ of the molecule as
$$
    m\ddot{x}_i = F_i(\textbf{r}^N) + F^{ext}_i
$$
where $F_i(\textbf{r}^N)$ is the force within the molecule on particle $i$. In $F^{ext}_i$ are all the other forces (intermolecular and potetials).
When the internal force is pairwise additive and a central force (force that acts along the connection line between the particles, always in point particles as they have no internal structure) then Newton's third law (actio = reactio) holds.

Now we can express the EOM of the molecule with its center of mass.
$$
    M\ddot{Q}(t) = F^{ext}
$$
where $F^{ext}$ is the total external force on the COM of the molecule
$$
    F^{ext} = \sum_{i=1}^n F_i^{ext}.
$$

We can ignore the internal forces as the sum for them vanishes because of Newton's third law.
With this the molecule can be handeled more easily in the simulation. Also usually only the angular momentum relative to the COM has to be considered. This is done by writing the movement of an atom of the molecule as the relative movement to the COM of that molecule and we can show that this holds
$$
    \frac{dL_r(t)}{dt} = \tau_r(t).
$$
where $L_r$ is the relative angular momentum of the molecule and $\tau_r$ is the relative torque exerted by the external forces wrt the COM of the molecule.
The total kinetic energies can also be decomposed into contributions of COM translation and contributions of the rotations. Here the rotational contributions are in terms of the relative movement of the atoms to the COM.
Each molecule is described by 3 degrees of freedom for the positions, 3 for the rotations and 3 for the momenta.

### How can we express the angular velocities?
We can write the decomposed velocities of an atom with the angular velocity operator, for which we can show that is has a one-to-one correspondence to the angular velocity (pseudo) vector. Then we can just use that vector to write the total and *translational velocities $\dot{x}(t)$?*. Using this we can also express the rotational kinetic energy in terms of the angular velocity vector and the inertia tensor which can be further simplified to 
$$
    K_r(t) = \frac{1}{2}L_r^T(t)\omega(t)
$$

### What is the importance of the Euler equations?
The solution of the Euler equations is the angular velocity vector in the moving frame given a torque in terms of the moving frame.
Using a solution $\omega$ we can write the kinematic equations
$$
    \dot{\mathcal{R}}(t)\mathcal{R}^{-1}(t) = \Omega(t) \equiv skew(\omega(t))
$$
which is a differential equation of the rotation operator. This fully specifies rotational motion.
The kinematic equation can be written in different parametrizations for $\mathcal{R}(t)$ like Euler angles or unit quaternions.

Euler equations are the newtonian EOM wrt of the COM, and one DEQ for the angular momentum.

### What are the properties of these parametrizations?
**Euler angles:** 
- evaluating many trigonometric functions is computationally expensive
- for the angles $\theta \in [0,\pi]$ the other angles are individually note well defined and the kinematic equation becomes singular

**Unit quaternions:**
- in this parametrization the kinematic equation is algebraic simple $\rightarrow$ no singularities
- the only drawback is the constraint
    $$ 
        |q|^2 \equiv 1
    $$
but there are ways around this eg. NO-SQUISH algorithm.

### What is another way of doing MD to consider the rotations of rigid molecules?
We can use constraint forces instead and carry out a MD simulation with these forces. These forces allow us also to model semi rigid molecules.

### How do constraint forces affect a molecule?
Imagine we have a particle that should move along a surface $f(r^N)=0$. For this initial velocity of the particle has to be perpendicular to the gradient of the function $\sigma$
$$
    \dot{\sigma} = \nabla \sigma \cdot \dot{r}
$$
however if the particle moves along this trajectory, the shape of the surface will change and $\nabla \sigma$ will differ too so the path of the particle will not be on the surface (tangent) anymore but move away from it, therefore we need a force that keeps the particle on the surface. This is the constraint force.

**Note:** Level surfaces $f(r^N) = c$ are the higher dimensional equivalent of the lines along a 3d surface that correspond to a specific value *("Aequipotentialflaechen")*. The gradient of the function $f$ is always perpendicular to these level planes.

Each constraint confines the motion of the system to a hypersurface of dimensions $(3N - 1)$, so for n constraints this would mean $d=3N - n$.

### How can we write the Lagrangian for system with constraints?
For a system with n constraints $\sigma_n(r^N) = 0$ we can express the Lagrangian as 
$$
    \mathcal{L}' = \mathcal{L} - \sum_{\alpha = 1}^n \lambda_{\alpha}\sigma_{\alpha}(r^N).
$$
Here the $\lambda_{\alpha}$ are the Lagrange multipliers. Expessing the EOM of this new Lagrangian in cartesian coordinates we get 
$$
    m_i \ddot{r}_i = F_i + \sum_{\alpha} G_i^{\alpha}
$$
with the constraint forces
$$
    G_i^{\alpha} = - \lambda_{\alpha}\nabla_i \sigma_{\alpha}.
$$
Due to the gradient of the surface these constraint forces are normal to the constraint (level) surfaces. The Lagrange multipliers are used to adjust these forces in order to keep the trajectory on the constraint surface.

### What are the conditions to find the Lagrange multiplier?
First we have to require two things:
1. The constraints don't change: $\dot{\sigma}_{\alpha} \equiv 0$
2. Their rate of change vanishes: $\ddot{\sigma}_{\alpha} \equiv 0$. This makes sure that motion of the system follows the shape of the constraint surface.

### Why are the exact Lagrange multiplier not very useful for doing MD?
This is because the Lagrange multiplier calculated in that way are specific to the exact EOM. Due to the nature of the MD simulations we follow an approximation of these EOM and the Lagrange multiplier mentioned above would not guarantee that the constraints are enforced correctly for this approximation of the EOM (difference equations).
Even if the constraint is obeyed up to order $\mathcal{O}(\Delta t^3)$ (in the case of a particle moving along the surface of a sphere where the constraint force is the centripetal force) this small error would grow exponentially for chaotic systems. [[ACP-MD-Hamilton-Mechanics#^Lyapunov-instability|Lyapunov Instability]]

### How can we calculate the Lagrange multiplier to use with numerical integrators?
*There exists a numerical iterative scheme described in script p. 277-278*

### Other iterative schemes
These can be used to get around the issue of calculating the Lagrange multiplier by directly solving the linear system of equations.
**SHAKE:** This is an algorithm similar to the Gauss-Seidel algorithm. Specifically designed for Verlet algorithm
**Rattle:** Designed for the velocity Verlet algorithm.
