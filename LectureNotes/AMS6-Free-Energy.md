Status: #LectureNote 
Tags: [[AMS]]

# AMS6 Free Energies

### Is the free energy unique?
No it's not. The free energy profile depends on the collective variable it is associated with. The free energy as a function of a collective variable is merely a projection to a lower dimension (by intgrating out degrees of freedom). The information lost depends on the choice of the collective variable. 

### How can we change the free energy and not lose information?
We can do this by transforming the collective variable. As shown in the image below.

![[Assets/img/collective_variable_free_energy.png]]

We can transform between the probability distributions for each of the collective variables [[AMS1_Introduction_and_Statistics#^pdf-compression|like so]]. This allows us to simplify the free energy landscape. We can then sample the PDF corresponding to the simpler free energy and then transform our collective variable back again.
This requires knowledge of a mapping (such as a transformation) between the collective variable of the simpler free energy and the collective variable of the complex one.

### How can we write the free energy as an ensemble average?
We can do that by using the trick of multiplying with one in our partition function in different ways.
1. Multiplying with $e^{\beta U(x)}e^{-\beta U(x)}$ we can write the free energy as an average of $\langle e^{\beta U(x)} \rangle$
2. Multiplying by $\frac{V^N}{V^N}$ we can interpret $1/V^N$ as the uniform distribution and we can write the free energy as $\langle e^{\beta U(x)} \rangle_{uniform}$. This can be further rewritten as an arithmetic mean, because the points are distributed accordingly.
3. Writing the free energy as a function of a collective variable
$$
    F\left(\hat{\xi}\right) = -k_BT ln\left(\langle \delta\left(\xi(\textbf{r}^N)\right) - \hat{\xi}\rangle \right)
$$

The caviat of this is that for all three options here the average is difficult to compute. Even for the uniform distribution exponential averaging is usually not feasible because the region in phase space that corresponds to the larger contributions is really small.

However we can show that exponential averaging over the uniform distribution corresponds to computing the free energy difference between our system and the ideal gas. And we find these connections:
$$
\begin{aligned}
    \langle e^{\beta U(\textbf{r}^N)} \rangle = e^{-\beta (F_{id} - F)}\\
    \langle e^{-\beta U(\textbf{r}^N)} \rangle_{uniform} = e^{-\beta (F - F_{id})}\\
\end{aligned}
$$

### What is the problem with exponential averaging with the normal distribution?
The problem is that the significant contributions that are very large have a small statisticar weight, ie. the probability to draw them is low. The contributions that are almost 0 are much more likely to be drawn. The statistical weight is given by the Boltzmann factor.
All contributions of x are equally important, because the integrand is 1:
$$
    \langle e^{\beta U(x)} \rangle = \int dx \frac{e^{-\beta U(x)}}{Q} e^{\beta U(x)} = \frac{1}{Q} \int dx \: 1
$$
*Because of this exonential averaging converges very slowly.*

### What do we use enhanced sampling methods for?
These are sampling methods that allow us to sample regions of configuration space that have a low probability to be visited by increasing the likelihood to find the system in such a state and dealing with the bias this procedure inflicts.
