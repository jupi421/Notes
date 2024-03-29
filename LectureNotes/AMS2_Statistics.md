Tags: #LectureNote [[Advanced_molecular_simulation]] 

# AMS2_Statistics

### What method is used to get the probability density from a non-invertible g(x)?
We can get it from a function of a specific variable. 
When $g(x)$ isn't invertible and has a countable number of roots $x_i$ where $y = g(x_i)$, we calculate [[AMS1_Introduction_and_Statistics#^pdf-compression|this expression]] for every $x_i$ and then sum over all results. The derivative is taken at each $x_i$.
This can be written as ^CPD-non-invert
$$ 
    f_Y(y) = \sum_i f_X(x_i) \left| \frac{dg}{dx} \right|^{-1}
$$

**Example:** [[Zettelkasten/Harmonic_Oscillator|Harmonic oscillator]] 
1. write the function of variable Y:
    $E(x) = \frac{1}{2} kx^2$
2. write the PDF of variable X down and normalize:
    $f_X(x) = \frac{1}{\sqrt{2\pi/k\beta}}exp(-\beta kx^2 / 2)$
3. rewrite X as a function of Y:
    $x = \sqrt{2E/k}$
4. plug it in [[AMS1_Introduction_and_Statistics#^pdf-compression|this expression]] and calculate the derivative $dX/dY$:
    $dx/dE = \sqrt{\frac{2}{k}} \frac{1}{2\sqrt{E}}$
5. now use [[AMS2_Statistics#^CPD-non-invert|this]]: 
    Because $E$ is symmetric, the values PDF for both $x_i$ are equal so after we add both contributions we get $dx/dE = \sqrt{\frac{2}{k}} \frac{1}{\sqrt{E}}$ and $f_E(E) \propto \frac{1}{\sqrt{E}} exp(-\beta E)$

### How do we get f_y(y) in terms of a Delta-Function? 
We can rewrite [[AMS2_Statistics#^CPD-non-invert|this]] in terms of a dirac delta function because

$$ 
    f_X(x_i) = \int_{-\infty}^{\infty} dx\: f_X(x)\: \delta(x-x_i)
$$
and it becomes
$$ 
    f_Y(y) = \sum_i \int_{-\infty}^{\infty} dx\: f_X(x)\: \delta(x-x_i) \left| \frac{dg}{dx} \right|^{-1}
$$
using the property of the dirac function
$$ 
    \delta(g(x)) = \sum_i \delta(x-x_i) \: \left| g'(x_i) \right|^{-1}
$$
where $x_i$ are the roots of $g(x)$, we can write the PDF $f_Y(y)$ as
$$ 
    f_Y(y) = \int dx \: f_X(x) \: \delta(y-g(x)).
$$
Note that $y = g(x_i)$.

This new notation allows us to write the PDF of $Y$ as an expectation value of the dirac function ^PDF-dirac
$$ 
    \langle \delta(y - g(x)) \rangle_X = \int dx \: f_X(x) \: \delta(y-g(x)).
$$

### What do we need this Formalism for?
[[AMS2_Statistics#^PDF-dirac|This]] can be used to evaluate the PDF of a variable $Y$ using the PDF of a variable $X$ it depends on if the mapping $g(x)$ from $x$ to $y$ is not invertible.

### When are multivariate distributions used?
[[Multivariate_Distributions|Multivariate Distributions]]

### Why are conditional probabilities not normalized
[[Zettelkasten/Conditional_Probabilities|Conditional Probabilities]] don't need to be normalized because

### How are conditional probabilities and marginal probabilities connected?
What happens when dividing by the marginal probability

### What are independent, identically distributed random variables?

### What is the covariance of two variables?

### Why is the covariance used in the higher dimensional Gaussian instead of the variance?

### What is the difference between the covariance and variance?

### What is the difference between being uncorrelated and being independent?
