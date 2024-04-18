Topic: [[Statistical-Physics]] [[Computational_Physics]]

# Linear response theory

By simulating systems we want to find the transport coefficients of the system. Linear response theory makes it possible to express these properties as functions of positions and momenta.

**More general:** The linear response theory provides a link between the time correlation function and the way the system responses when disturbed slightly. 

## Static response

When the system is perturbated by a weak field and we are interested in an observable that can be expressed as an average of a dynamical variable. We can write the change of that variable as
$$ 
    \langle A \rangle' = \langle A \rangle_0 + \langle \Delta A \rangle
$$
We can also say that this perturbation corresponds to a change in energy by a small amount
$$ 
    \Delta H(\Gamma) = \lambda B(\Gamma)
$$
where $\lambda$ is a homogeneous and time-independent field.

Now $\langle A \rangle'$ can be written as the average of $A$ with the new energy. The change of $A$ can be written as
$$ 
    \langle \Delta A \rangle \approx \lambda \left( \frac{\partial \langle \Delta A \rangle}{\partial \lambda} \right)_{\lambda = 0} 
$$
because the perturbation is so small we can assume it is similar as the infinitessimal change of $\langle A \rangle$ at $\lambda = 0$ i.e. without field, **showing that this small perturbation is really similar to the fluctuations of $A$ in equilibrium**.
Evaluating this derivative shows that the linear response of an observable in a weak field is completely determined by the equilibrium averages in no field.
$$ 
    \langle \Delta A\rangle = \lambda \beta \left[ \langle AB \rangle_0  - \langle A \rangle_0 \langle B \rangle_0 \right]
$$

**Note:** This can be applied to any observable even $B$ (the one that couples the perturbation with the system). If A and B are uncorrelated turning on the field hos no effect on A.

## Dynamic response

Dynamic response is when the system is pertubated like in the case of the static response and has enough time to equilibrate, then the field is turned off and the system is observed how it relaxes back to it's original state again i.e. $\langle \Delta A \rangle = 0$. We set the time $t=0$ when we turn off the perturbation.

#### TODO
add pictures of dynamic linear response. Script p.170

We can now do the same things as in the static response, just with $A(t)$ now being time-dependent. Calculating $\langle A(t) \rangle$ results in
$$ 
    \langle \Delta A(t) \rangle = \lambda \beta \left[ \langle B(0)A(t) \rangle_0 - \langle A(t) \rangle_0  \langle B (0) \rangle_0 \right]
$$
which can be simplified to
$$ 
    \lambda \beta \langle \Delta B(0) \Delta A(t) \rangle_0
$$
This shows that the response to a time-dependent perturbation of the system in described by the equilibrium time correlation function of the unperturbated system.
