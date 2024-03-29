Topic: [[Zettelkasten/Statistics_and_Probabilities]]

# Marginal_Distribution

The marginal distribution is calculated by integrating one or more degrees of freedom out of a [[Multivariate_Distributions#^joint-prob-dist|joint probability distribution]]. This results in the total probability of the variables $x_1, ... , x_m$ considering all values of the variables $x_{m+1}, ... , x_n$ that have been integrated out.
For $m < n$ we can denote the marginal probability distribution as follows:
$$ 
    f_{X_1,...,X_m}(x_1,...,x_m) = \int dx_{m+1}...dx_n \: f_{X_1,...,X_n}(x_1,...,x_n)
$$
