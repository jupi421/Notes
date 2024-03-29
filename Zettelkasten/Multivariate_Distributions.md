Topic: [[Statistics_and_Probabilities]]

# Multivariate Distributions

Multivariate distributions are probability distributions that depend on more than one variable.
One example is the joint cumulative distribution
$$
    F_{X_1, X_2, ... , X_n} (x_1, x_2, ... , x_n) = P(X_1 \le x_1, X_2 \le x_2, ... , X_n \le x_n)
$$
with the properties
$$ 
\begin{aligned}
    F_{X_1, ..., X_n} (-\infty, -\infty, ... , -\infty) = 0\\
    F_{X_1, ..., X_n} (\infty, \infty, ... , \infty) = 1\\
\end{aligned}
$$

The PDF can be calculated by taking a [[Zettelkasten/Multivariate_Derivatives|derivative wrt all variables]] ^joint-prob-dist
$$ 
    f_{X_1, ... , X_n} (x_1, x_2, ... , x_n) = \frac{\partial^n}{\partial x_1 ... \partial x_n} F_{X_1, ... , X_n} (x_1, x_2, ... , x_n)
$$
which is the joint PDF. This is the probability that $x_1\in[x_1, x_1+dx_1]$ and similar for the other variables.

The average is computed analogous to the averages in single variate distributions, but integrating over all variables.
