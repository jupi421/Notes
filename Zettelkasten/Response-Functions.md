Topic: [[Linear-Response-Theory]] [[Statistical-Physics]]

# Response functions

This is a generalization of the [[Linear-Response-Theory|linear response theory]] to include perturbations that have arbitrary time dependences. In this case we can write the energy just as in the static response as
$$
    H(\Gamma, t) = H_0(\Gamma) - f(t)B(\Gamma).
$$

If we say that $f(t)$ is a linear response, then following relation must hold
$$ 
    \langle \Delta A(t, \lambda f) \rangle = \lambda \langle \Delta A(t, f) \rangle
$$
where $\lambda$ is a constant. This means that the response is proportional to the strenght of the perturbation.

The most general form consistent with this is 
$$ 
    \langle \Delta A(t, \lambda f) \rangle = \int_{-\infty}^{\infty} dt' \chi_{AB}(t,t') f(t')
$$
where $\chi_{AB}$ is the response function.

**This response function should obey following:** ^response-function-properties
1. *Causation:* There should be no response before the perturbation, hence $\chi_{AB}(t,t') = 0 \text{ for } t < t'$.
2. *Time translational invariance:* It should only depend on time differences not on specific time stamps because it is an equilibrium property.

Using these propenties we can now write the response function as 
$$ 
    \langle \Delta A(t, \lambda f) \rangle = \int_0^{\infty} d\tau \chi_{AB}(\tau) f(t - \tau)
$$
where $\tau = t - t'$.
Knowing the response function makes it possible to calculate the response to an arbitrary perturbation.

Using the properties of the mirrored Heaviside-step function and the above relation, we can show that the response function can be found by
$$ 
    \chi_{AB}(t) = -\beta \frac{d \langle \Delta B(0) \Delta A(t) \rangle_0}{dt} \theta_H(t)
$$
