Status: #LectureNote
Tags:

# ACP-MD-Numerical-Integrators

### What did we investigate the symmetries and properties of Hamiltonian mechanics for?
We did that because these are the mechanics of the EOM we use in MD the numerical integrators should preserve these symmetries (ie. time reversability and symplecticity).

### What are the explicit requirements for the numerical integrators?
^time-reversability **Time reversability:** For the exact flow of the Hamiltonian we have the time reversability condition
$$
    \phi_t \circ \mathcal{T} \circ \phi_t = \mathcal{T}.
$$
For a small time step this becomes
$$
    \phi_{\Delta t} \circ \mathcal{T} \circ \phi_{\Delta t} = \mathcal{T}.
$$
or
$$
    \phi_{\Delta t} \circ \mathcal{T} \circ \phi_{\Delta t} \circ \mathcal{T} \phi_{\Delta t} = \mathbb{I}.
$$

**Symplecticity:** The symplecticity condition can also be applied to the small time step
$$
[\partial \phi_{\Delta t}]^T \cdot \mathbb{J} \cdot \partial \phi_{\Delta t} = \mathbb{J}
$$

### Are the discussed numerical integrators time-reversible and symplectic?

| Algorithm | supports time reversability |
|:---|:---|
| Euler | no |
| Velocity Verlet | yes |
| Verlet | yes |
| PC | no |
| Runge Kutta | no |

Velocity Verlet is symplectic for all degrees of freedom.

### What are splitting methods?
With splitting methods one can derive time-reversible and symplectic algorithms for MD simulations based on the Liouville formulation of classical mechanics.
The Liouville formulation gives insight into the energy stability of algorithms and can also be used to derive multi-time-step algorithms.

1. write the Liouville operator for the coordinates used in the Hamiltonian.
2. split Liouville operator into momentum and configuration part (Trotter identity)
3. expand it as a series and see how this affects a vector if it's applied to it.
4. do this for each individual Liouville operator.
5. check for time reversability and symplecticity.

With this approach we can derive the velocity verlet, adjoint velocity verlet(half kicks and full steps switched), symplectic euler and adjoint symplectic euler as well as multi-time-step algorithms. This is done with changing the way how the exponential Liouville operator is approximated (for adjoint: switching the sequence of the individual Liouville operators).
Symplectic Euler is not time-reversible. 

### Why is it so important that the numerical integrators are symplectic?
Because these integrators are symplectic it means that they describe a symplectic flow (which implies phase space conservation). A Hamiltonian can be reconstructed up to a constant from a symplectic flow, so we can assume that there is a corresponding Hamiltonian for the flow symplectic integrators describe. 

### What are shadow Hamiltonian?
These are the Hamilton functions that correspond to the symplectic integrators. Ideally the shadow Hamiltonian of an integrator should be as close as possible to the actual Hamiltonian of the system. This would make the integrator a good fit to use on the system.
One can show that the trajectory produced by the symplectic integrator with the same initial state is the exact same as the trajectory produced by the shadow Hamiltonian, which is just different by a constant. This is also the reason why the symplectic algorithms don't show long time energy drifts.
Also the shadow Hamiltonian is strictly conserved along the trajectory of the velocity Verlet while the actual Hamiltonian fluctuates. This is not a problem if the time steps are sufficiently small, because then the difference between the shadow Hamiltonian and the Hamiltonian is also small.

### What does the shadow Hamiltonian depend on?
It depends on the specific integrator that is used. For the velocity verlet the difference to the original Hamiltonian is of order $\mathcal{O}(\Delta t^2)$, this also requires the potential energy to be at least differentiable twice. 

### Are the results obtained by the trajectory of the shadow Hamiltonian useful to describe the dynamics of the system?
This depends on the quantities we're interested in. If the quantities are very sensitive to the difference in the Hamiltonian, then this will not produce a good result. Usually the microcanonical averages of a phase space variable are not sensitive to small changes in the Hamiltonian and we can expect good results for the statistical averages and the correlation functions.
Quantities like the end points of the trajectory are very sensitive.

### What are some use cases of the shadow Hamiltonian itself?
The variance of the energy is of order $\mathcal{O}(\Delta t^4)$ then the root mean square fluctuation of the energy $\sigma_E$ is of order $\mathcal{O}(\Delta t^2)$. Plotting this against $\Delta t^2$ results in a line trough 0. With this we can debug our MD simulation. 
Another usecase is to use this to determine a good time step. This is done by selecting a time step for which this plot is linear.

We can also calculate the quantities of interest for two or more time steps in that linear regime and then fit a line to get an estimate of the quantities for the exact trajectory.

### What is the purpose of multi-time-step algorithms?
In the case of fast(intermolecular vibrations) and slower (intramolecular motion) motions the slower ones don't change very much on the time scale of the faster time scale, so computing the intramolecular forces every step is not needed. Multi-time-step algorithms allow to treat fast and slower motions in their time scales respectively. This is done by calculating these with different time steps which can speed up the simulation.

To derive this we do the same as for the other integrators just that instead of $\mathcal{L}_r$ and $\mathcal{L}_p$ we split it into $\mathcal{L}_{fast}$ and $\mathcal{L}_{slow}$. This results in a RESPA algorithm. Aside from it's advantages it's disadvantage is that different potential components are decoupled. This can cause severe artifacts. 
