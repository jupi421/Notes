Topic: [[Statistics_and_Probabilities]]

# Conditional Probabilities

This is the probability $f(x_1 | x_2)$ of $x_1$ under the condition that another (or more) variable $x_2$ is fixed at a specific value and is proportional to the [[Multivariate_Distributions|multivariate distribution]].
$$ 
    f(x_1|x_2) \propto f(x_1, x_2)
$$
So we can say that they are similar up to a constant $A$.
$$ 
    f(x_1|x_2) = A \: f(x_1, x_2)
$$
Now we can calculate the constant by integrating wrt $x_1$ as we keep $x_2$ fixed, because this constant is the normalization. 
$$ 
    \int dx_1 \: f(x_1|x_2) = A \int dx_1 \: f(x_1, x_2)
$$
The right hand integral is just the marginal probability distribution of $x_2$ so the constant has to be $f_{x_2}(x_2)$.

**The conditional probability is just the joint probability divided by the marginal probability of the fixed variable.** This applies to multivariate distributions as well.

Conditional averages exist as well. One way to express them is by using delta functions:
$$ 
    \langle \Phi(x_1, x_2) \rangle_{x_2} = \frac{\langle \Phi(x_1, x_2) \: \delta(X_2 - x_2) \rangle_{x_2}}{\delta(X_2 - x_2)}
$$
This just means that in the average all values of $\Phi$ should be taken into account where $X_2$ is set to a specific value $x_2$. 
