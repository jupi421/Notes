Status: #LectureNote
Tags:

# ACP-MD-Other-Ensembles

### How can we sample different ensembles other than the microcanonical ensemble in MD?
Either modify the EOM or combine time evolution obtained by Newtons EOM with appropriate stochastic steps.
These approaches modifies the dynamics of the system. It doesn't matter for static averages but you have to consider this when interpreting the dynamics with eg time correlation functions.

### What do we use thermostats for?
We use them to do simulations with constant temperature or to remove dissipated heat from a system in non-equilibrium (heatbaths/heatsink).

### What is the Andersen thermostat?
The Andersen thermostat is a thermostating mechanism that produces a canonical ensemble for a given temperature by coupling the system to a heat bath. This is realized by occasionally adding an impulse to a random particle.
In such a stochastic collision a velocity that corresponds to the desired temperature is drawn from a Maxwell-Boltzmann distribution and given to a random particle. These collisions can be seen as a MC step. The strength of the heatbaths-system coupling can be controlled by the collision frequency $\nu$. In other words we are mixing Newtonian dynamics with stochastic collisions.

### How do we integrate that into our MD simulation?
1. Initialize System
2. Integrate EOM according to the numerical integrator
3. Andersen thermostat: Loop over all particles, select each one with probability $\nu \Delta t$, assign to each selected particle a velocity drawn from the Maxwell-Boltzmann distribution for the target temperature 
4. go back to 2.

Repeated application of the Andersen algorithm produces a canonical distribution.

### What are the drawbacks of the Andersen algorithm?
- Having these stochastic collisions suddendly decorrelate the velocities and make the dynamics discontinuous. This is not realistic! To get information about the dynamics of the system, we have to pick the collision frequency accordingly (high enough to sample the canonical ensemble, small enough to not disturb the dynamics significantly). *Rule of thumb: Select $\nu$ so that it doesn't reduce the diffusion constant significantly*
- Because the collisions are random the dynamics can't be reproduced exactly
- no well defined conserved quanities that can be monitored to guarantee consistency of the simulation

### What is the Nose-Hoover thermostat?
This thermostat does not rely on a stochastic process, istead an additional degree of freedom is introduced. This checks if the temperature differs from the target temperature and then scales the velocities of the particles accordingly.

### How does this affect the Hamiltonian?
It is implemented using an extended Hamiltonian/Lagrangian:
$$
    H_N(\textbf{r}^N,\textbf{p}^N,s,p_s) \equiv \sum_{i=1}^{N} \frac{\textbf{p}^2_i}{2m_is^2} + U(\textbf{r}^N) + \frac{p_s^2}{2Q} + gk_BTln(s)
$$
Here $Q$ determines how quickly the thermostat reacts and $g$ is selected in a way that the microcanonical distribution in the extended phase space (regular phase space with the 2 new dimensions) corresponds to a canonical distribution in the original phase space, $s$ is the rescaling factor that acts as the thermostat and $gk_BTln(s)$ is needed to obtain the canonical distribution in the original phase space. This last term is used to control the temperature of the canonical distribution, whereas $s$ and $p_s$ can be seen as the thermostating mechanism and even that it doesn't affect the distribution in physical space (original phase space) $p$ is needed to obtain a microcanonical distribution from the extended Hamiltonian.

The EOM obtained from this Nose Hamiltonian can be further simplified by introducing a friction term $\xi$. The resulting Hamiltonian is the *Nose-Hoover Hamiltonian*, which can be monitored to assure that the algorithm is correct as this quantity has to be preserved.

### What are the Nose-Hoover EOM?
$$
\begin{aligned}
    \frac{dr_i}{dt} = \frac{p_i}{m_i}\\
    \frac{p_i}{dt} = F_i - \xi p_i\\
    \frac{d\xi}{dt} = \frac{1}{Q} \left\{ \sum_{i=1}^N \frac{p_i^2}{m_i} - 3Nk_BT\right\}\\
    \frac{dlns}{dt} = \xi
\end{aligned}
$$

### How does the Nose-Hoover thermostat control the temperature?
In the 3. EOM represents the thermostat mechanism ($3Nk_BT$ represents $\langle 2K \rangle$ and the sum for the kinetic energy) 
$K$ is the instantaneous kinetic energy
- $K > \langle K \rangle$ for the target temperature $T$ then the right side of the EOM for $\xi$ is positive resulting in the thermostat variable to increase. This leads to the thermostat to reduce the velocities by velocity-dependent forces that point against the direction of the velocities and decelerate the particles. 
- analogous for the other case

This leads to the instantaneous kinetic energies to fluctuate, but over time the average will converge towards the kinetic energy corresponding to the target temperature.

The thermostat doesn't react instantaneously to deviations in the instantaneous temperature, the time derivative of the friction variable does. This effect then propagates to the friction variable which can be seen as an average over time. This is called an integral feedback.
The latency of the thermostat can be controlled by tweaking the thermal inertia parameter $Q$. If it is small then the thermostat reacts quickly. $Q$ should be chosen in a way that the dynamics of the system is not disturbed too much. To check how much the thermostat affects the system we can look at the velocity autocorrelation function.

### What integrators can we use for the Nose-Hoover EOM?
Because the transformation of the variables used in the derivation of the Nose-Hoover EOM are not canonical, the EOM can't be derived from a Hamiltonian and thus are not symplectic. That's why we can't use the same integrators.We can integrate these either with Runge-Kutta schemes or derive a Nose-Pointcare Hamiltonian that is closely related to the $H_{NH}$ and can be integrated with symplectic algorithms.

### What are Nose-Hoover chains?
Sometimes the Nose-Hoover thermostat can't sample the canonical distribution because the dynamics are not ergodic (can happen when there are stiff degrees of freedom in the system). In this case one can chain multiple Nose-Hoover thermostats together, where only the first thermostat in the chain interacts with the system directly. That's why calculating the others is computationally really cheap.

### What is the Berendsen and Bussi-Donadio-Parinello thermostats? 
These thermostats have similar feedback principles as the Nose-Hoover thermostat.
Eg. the Berendsen thermostat rescales the velocities in such a way that the rate of change of the instantaneous temperature is proportional to the difference of the instantaneous and target temperature. The fluctuations in the kinetic energy is not compatible with the canonical ensemble and that's why it will sample these wrongly.
*More on that script p. 297*

### How do we do MD in the NpT ensembles?
Here again we will introduced an extended Hamiltonian. The basis for this is to first derive the EOM for the isenthalpic-isobaric NpH ensemble. In the NpT ensemble the enthalpy then fluctuates and the temperature is imposed.
In the NpH ensemble the volume is introduced as a dynamic variable.
These EOM are given by
$$
\begin{aligned}
    \dot{r}_i = \frac{\textbf{p}_i}{m_i} + \frac{1}{3}\frac{\dot{V}}{V}r_i\\
    \dot{p}_i = F_i - \frac{1}{3}\frac{\dot{V}}{V}p_i\\
    \dot{V} = \frac{pv}{W}\\
    \dot{p}_V = \frac{1}{3V} \sum_{i=1}^N \left[\frac{p_i^2}{m_i} F_ir_i\right] - p
\end{aligned}
$$
Scaling the volume directly couples to the positions and momenta.
This represents the isenthalpic-isobaric barostat.

To do MD simulations in the NpT ensemble now we have to couple this barostat with a thermostat and efficient integrators can be derivede by the Liouville formalism.
