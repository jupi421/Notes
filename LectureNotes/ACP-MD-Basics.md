Status: #LectureNote 
Tags: 

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
