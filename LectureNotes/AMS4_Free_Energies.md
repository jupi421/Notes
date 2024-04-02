Status: #LectureNote
Tags:[[Advanced_molecular_simulation]]

# AMS3_Free_Energies

### How does splitting $Q_{NVT}$ into $Q^{(id)}$ and $Q^{(ex)}$ affect $F(N,V,T)$?
The free energies for the ideal and the excess part are added. Here $F^{(id)}$ represents the free energy of the ideal gas. [[Zettelkasten/Partition_Function|More on partition functions]].

### Why does adding a constant to the energy not affect the free energy?
Because when adding a constant to the energy this translates to adding that constant to the free energy. As we're only interested in the energy differences between two states, the constant cancels.

### What is a control parameter?
A control parameter $\lambda$ is a factor that we use to scale the potential energy. These are macroscopic variables like volume, strenght of an electric field or temperature.

### Why do we express the free energy as a function of the control parameter?
We do this to scale the energy of the system. For a system being examined in two states of different volume the free energy has no information about the difference in volume, which can be scaled accordingly with the control parameter.

### Diagramm of config space
#### TODO

### What is a characteristik/indicator function?
This offers to write the partition function as an integral over the entire configuration space and not only over a region. It is defined as
$$ 
h(r^N) = 
\begin{cases}
    1 \text{ if $r^N \in A$}\\
    0 \text{ otherwise}
\end{cases}    
$$

### How are [[Free_Energies|free energies]] connected to probabilities?
The free energy is connected to probabilities in the way that when the free energy is minimized it translates to the state with the highest probability. The free energy difference between two regions in configuration space determines their relative probability to occur.
$$ 
    \frac{P_A}{P_B} = \frac{\langle h_A \rangle}{\langle h_B \rangle} = \frac{\langle Q_B \rangle}{\langle Q_A \rangle} = e^{-\beta \Delta F}
$$

### Coexistance in context of $P_A/P_B$ has to be 1 -> free energy?
Because the probability is the same to find the system in both regions.

### Is a 2nd order phase transition sharp?
#### TODO

### Why doesn't $T$ play a role in the hard sphare system (purely entropic system)?
The Bolzmann factor for the hard spere system is given by
$$ 
    e^{-\beta U(r^N)}
$$
with the energy
$$ 
U(r^N) =
\begin{cases}
    0 \text{ if no overlap}\\
    \infty \text{ if overlap}
\end{cases}
$$

So the temperature in $\beta$ can be neglected because the energy is either $0$ or $\infty$.
