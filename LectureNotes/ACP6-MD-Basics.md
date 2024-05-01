Status: #LectureNote 
Tags: [[Zettelkasten/Numerical-Integrators]]

# ACP-MD-Basics

### What is MD and how does a typical MD simulation look like?
A typical [[Molecular_Dynamics|molecular dynamics]] simulation is similar to an actual experiment:

| **Molecular Dynamics** | **Experiment** |
|:---|:---|
| prepare system in specific state | prepare sample | 
| run simulation following EOM | measure properties of interest |
| longer simulations (more data) less statistical errors | more data -> less statistical errors | 

### What is the difference between the 3 formalisms of mechanics (Newton, Lagrange, Hamilton)?
[[Zettelkasten/Newton-Mechanics|Newton Mechanics]]: For simple problems with few bodies, forces are easy to identify and work with, simple geometries. 
Because of
$$ 
F(r^N) = -\nabla_i U(r^N) = -
\left(
\begin{array}{c}
    \frac{\partial U(r^N)}{\partial x_i}\\
    \frac{\partial U(r^N)}{\partial y_i}\\
    \frac{\partial U(r^N)}{\partial z_i}\\
\end{array}
\right)
$$
Newton's EOM result in a system of 3N coupled ordinary differential equations. They are coupled because the force on one particle is dependent on the positions of all the other particles.

[[Zettelkasten/Lagrange-Mechanics|Lagrange Mechanics]]: For problems including many particles and/or constraints. Using the Lagrange mechanics to describe the system results in a set of second order differential equations. Solving these equations we can find the generalized trajectory $\{q(t)\}$ of the system.

[[Zettelkasten/Hamilton-Mechanics|Hamilton Mechanics]]: Useful when studying phase space or when transitioning from classical to quantum mechanics. We use this to simplify the EOM from the Lagrange mechanics to a system of first order differential equations.

### What are the possible conservation laws in a system used for MD?
1. If the Hamiltonian has no explicit time dependence: The total energy is conserved
    $$ 
        \frac{dH}{dt} = 0
    $$
2. If the potential energy is also invariant to translations: Total (linear) momentum conserved.
    $$ 
        P = \sum_{i=1}^N p_i
    $$
3. Without [[Zettelkasten/Periodic-Boundary-Conditions|PBC]] the angular momentum
    $$ 
        L = \sum_{i=1}^N r_i \times p_i
    $$
is conserved as well. PBC break ratational invariance.

### What othere benefits does using Hamilton mechanics have?
- Allowing for time reversability meaning that if the signs off all momenta are flipped, the system goes back in time along the same trajectory.
- It follows [[Zettelkasten/Liouvilles-Theorem|Liouville's theorem]].


### How are macroscopic measuments and relate to enseble averages?
Given the small time scales in MD simulations when measuring something with a measurement device it relates to taking the time average of that quantity.
Because in MD the energy is conserved and in the microcanonical ensemble the energy is constant we use that ensemble. In case the system is [[Zettelkasten/Ergodicity|ergodic]] the time average is the microcanonical ensemble average.

**Hint:** Here ergodic means that with sufficient time, the system comes arbitrarily close to any point on the energy shell, i.e. visits every configuration with the specified enegy.

### Why can we neglect the [[Zettelkasten/NVEP-Ensemble|NVEP]] ensemble?
Because in MD the system is not moving most of the time, so $P=0$. Also the differences between NVE and NVEP are usually minor.

### How can we simulate a system with a specific temperature?
Usually with trial and error the energy is adjusted to correspond to the desired temperature. Calculating the temperature of the system is done by averaging over the *instantaneous temperature*
$$ 
    T_K = \frac{2K}{3Nk_B}
$$
where $K$ is the kinetic energy.

**Note**: The heat capacity for constant volume can be calculated from the fluctuations of either the potential or the kinetic energy.

### What are correlation functions?
Because [[Zettelkasten/Correlation-Functions|correlation functions]] used to study the dynamics of a system. 

### What makes the autocorrelation function so important?
Autocorrelation functions connect the thermodynamics of a system to [[Zettelkasten/Transport-Coefficient|transport coefficients]].

### What is the linear response theory?
[[Zettelkasten/Linear-Response-Theory|Linear response theory]] is the link between time correlation functions and the response of the system to weak perturbations.

### What are Green-Kubo relations?
These link an equilibrium property with the way the system relaxes after being perturbated via a correlation function.

### What is the purpose of response functions?
It generalizes the formulation of the linear response theory to account for fields of arbitrary time dependence.
More here: [[Zettelkasten/Response-Functions|response functions]]

### How are response functions and delta functions connected?
Response functions are just linear superpositions of delta impulses $f(t_0)\delta(t-t_0)$

### Explain the example of the movement of a molecule in an external field
1. Write the Hamiltonian according to response function
2. We're interested in the response of the average velocity observable which is completely determined by the response function
3. Calculate the response function
4. Due to time translational invariance the integrand for calculating the average of the velocity can be replaced by the autocorrelation function for the velocity.
5. Comparing this to the general definition for the velocity results in the Green-Kubo relation for the mobility of the particle.

**Summing up:** Write down the perturbated energy, then find the general definition for the quatity of interest, find the equivalent expression for calculating that quantity via response functions. Find a way to write that in terms of a autocorrelation function and compare it to the general definition to find the Green-Kubo relation.
*More here:* Computational Physics script p.174

### What methods are used to obtain the diffusion constant?
**Slope**
Plot the mean squared displacement averaged over all particles as a function of time. For diffusion the graph shows linear growth and the slope corresponds to around $6D$. For $t->\infty$ the slope is exactly $6D$.

**Einstein relation**
This is the link between the diffusion constant and the mobility. It is derived by comparing the Green-Kubo relations for the diffusion constant and the mobility:
$$ 
    \mu = \frac{D}{k_BT}
$$
This relates the diffusion constant to the mobility at a given temperature.

*Note:* For very dilute systems this autocorrelation function should show a monontonous exponential decay.

### What is the Backflow and cage effect?
**Cage effect:** The cage effect creates negative values for the autocorrelation function on short time scales, because in dense systems the particles bump into the nearest neighbors first before everything "loosens up" and they can diffuse more freely.

**Backflow effect:** Even at intermediate densities the average decay is not exponential but algebraic. This is because when the particle travels through the liquid it leaves microscopic vortices behind, which take away some of its momentum. This is a collective effect and it leaves behind some memory of the movement of the particle, which can be observed in the correlation function. This has very strong consequences on calculating the diffusion constant as in decays much slower.

### How can Fourier transforms make it easier to calculate the time correlation function of two observables?
The Fourier transform of the time correlation function is the same as the product of the Fourier transforms of the observables
$$ 
    \widetilde{C}_{AB} = \widetilde{A}^*_m \widetilde{B}_m
$$

To calculate the time correlation function we
1. calculate the Fourier transforms of the time series of $A$ and $B$
2. multiply the the transformed series
3. calculate the inverse transform of this prodict, which will be the time-correlation function

### What is the complexity of this way of calculating the time-correlation function?
Because we can use the FFT algorithm calculating the time-correlation function is of order $\mathcal{O}(M)$ as the FFT is of order $\mathcal{O}[M\:ln(M)]$.

### What is the Wiener-Khinchin theorem?
This relates the autocorrelation function to the power spectrum of the observable *(derived by calculating the time-correlation function of $A$ and $A$)* and is written as
$$ 
    \widetilde{C}_{AB}(m) = \widetilde{A}^*_m \widetilde{A}_m = \left| \widetilde{A}_m \right|^2
$$

### List the pros and cons for the different integration schemes?
#### Not to use

**Simple Euler:** No time reversability, does not conserve phase space volume ([[Liouvilles-Theorem]]), very large energy drift

#### Can be used
**Verlet Algorithm:**

| **pro** | **contra** |
|:--- |:--- |
| simple and low on memory | not self starting as knowledge of $r_i(-\Delta t)$ is required not only $r_i(t)$ |
| conserves total energy very well | velocities are in lower accuracy |
| fluctuations in energy only on small time scales  | numerical errors because of adding small numbers (velocity) to the difference of a large numbers (position difference) |

**Leap Frog:**
Improving the accuracy of the velocities by calculating them at half-time steps

| **pro** | **contra** | 
|:---|:---|
| numerically more ideal because no small and large numbers are getting added | velocities and positions not known at the same time -> total energy cannot be computed |
| velocities exlicitly in the algorithm -> adjusting the total energy in initialization easier |

#### Best to use
**Velocity Verlet:** 
1. compute new position
2. computed forces at new positions
3. compute velocities

| **pro** | **contra** | 
|:---|:---|
| conserves energy very well (because conserves phase space volume) | cannot be used for velocity-dependent forces because forces have to be calculated before the velocities
| self starting |

It is the same scheme as Verlet algorithm, but velocities have higher accuracy. Positions with error $\mathcal{O}(\Delta t^4)$ and the velocities with error $\mathcal{O}(\Delta t^3)$ => Velocity Verlet is over entire phase space a second order algorithm.

### What are some higher order algorithms that can be used for MD?
-Higher accuracy -> allow larger time steps
-not phase space volume conserving or time reversible

**Predictor-Corrector schemes:** 
1. Use the information of the position and the first $n$ derivatives (positionsa are the $0^{th}$ derivative) to predict the positions for the next time step along with the derivatives
2. Calculate forces
3. Find the deviation of the predicted accelerations and the ones corresponding to the calculated forces
4. Use this information to correct the predictions

Force evaluations for each time step are expensive -> not ideal to run until self consistency

**Runge-Kutta schemes:** 
- not time reversible
- don't conserve phase space volume -> long time energy drifts
- require multiple force calculations per time step

### What are Verlet lists and why do we use them?
Verlet lists can be used to reduce CPU time. 
These are lists of neighbors of a particle, in other words a list of particles that lie within a shell of radius $r_v = r_c + \delta$ and thickness $\delta$. By using these only the particles in the list have to be considered in force calculations reducing this operation to a complexity $\mathcal{O}(N)$.
Because the particles are moving in the system we have to check at every time stamp if the maximum displacement allows particles from outside $r_c$ to penetrate into $r_v$. In the case that two particles are on collision course we update the verlet list if
$$ 
    \Delta_{max}(k) \coloneqq \frac{\delta}{2}
$$
the maximum displacement is relative to the positions of the particles at the time of the initialization or the last update of the Verlet list. This means every time the list gets updated a snapshot of all particle positions has to be created and stored until the lists are updated again.

The shell thickness $\delta$ determines the frequency of the list updates. If it's too large, then there are many unneccessary particles in the lists, if it's too small, then the lists have to be updated more frequently which comes with the cost going by $\mathcal{O}(N^2)$. Best would be to optimize for $\delta$ in a trial run.

### What are cell lists and what benefits do they have over using Verlet lists?

Another method to save CPU time.
The cell is divided into subcells around the size of the cutoff radius. Then a particle can only interact with particles within it's own or the neighboring cells *(9 in 2d and 27 in 3d)*.
Assigning the particles to the subcells goes with $\mathcal{O}(N)$ compared to the complexity of creating and updating the Verlet lists.

**Note:** The subcell index for a particle with coordinates $(x, y, z)$ is given by $[x/r_c][y/r_c][z/r_c]$

### What time step should be used for a MD simulation?

Usually the time step should be smaller than the fastest degree of freedom.
- If too large it may not conserve energy well
- If too small, better energy conservation but many more iterations needed

| **System** | **smallest time scale** | **$\Delta t$** |
|:---|:---|:---|
| atomic fluid | mean time between collisions | ~10fs |
| molecular system | molecular motion/bond vibrations ... | for bond vibrations 0.5-1fs or 2-5fs for rotational degrees of freedom |
