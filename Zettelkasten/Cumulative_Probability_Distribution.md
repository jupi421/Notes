# Cumulative Probability Distribution

This is the probability that a random variable $X \le x$ than the value $x$.
It is denoted by 
$$ 
    F_X(x) = P(X \le x)
$$
and has the bounds $F_X(-\infty) = 0$ and $F_X(\infty) = 1$.
The derivative of the CDF is the probability density.

If g is an invertible function $F_Y(y)$ can be rewritten to 
$$ 
    F_Y(y) = P(Y \le y) = P(x < g^{-1}(y) = F_X(g^{-1}(y)))
$$
for **increasing** g and analogous
$$
    F_Y(y) = 1 - F_X(g^{-1}(y))
$$
for **decreasing** g. Here g is a function $g: \mathbb{ R } \rightarrow \mathbb{ R }$.
This works because we define $Y = g(x)$. So we can express the condition $Y \le y$ in x: $x \le y=g^{-1}(x)$.
