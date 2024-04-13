Status: #LectureNote
Tags: 


# AMS5-Free-Energies

### Why are first order phase transitions sharp?
Because the probability for one phase gets so much larger than the other one the further you move away from the coexistance line you go.

### What are collective variables/functions?
Collective variables are variables that depend on other variables, like the distance $r=\sqrt{(r_1 - r_2)^2}$. 

### What do we need the collective variables for?
These can be used to define regions in phase space which then can be used to write the [[AMS4_Free_Energies#^characteristic-function|characteristic function]] in that region.

With the characteristic functions in terms of the collective variables we can write the partition functions of a  region between two collective variables. 

### What is the purpose of writing the partition function as partition functions of thin shells in the area between the collective variables?
This allows for defining the free energy in a thin shell, which can be useful if we want to write the energy difference of two regions in phase space -> eg. two energy minima *(see example NaCl in water)*. This can then be used to calculate the required work to move from one region to the other.

### Why deos the free energy of a thin shell in configuration space diverge when the shell thickness goes to 0?
This happens because of the logarithmic term in the free energy that is dependent on the infinitessimal width $d\xi'$ of the thin shell. As the thickness goes towards 0, then the logarithm and as a result the free energy diverge.

### Why is this not a problem for?
It is not a problem as we are only interested in the free energy differences of the two regions and this factor cancels. This is why we can just ignore this term and write the free energy profile as
$$ 
    F(\xi) = -k_B ln(Q(\xi))
$$
and with multiple collective variables it is
$$ 
    F(\widehat{\xi}_1, ... , \widehat{\xi}_n) = -k_BT ln(Q_(\widehat{\xi}_1, ... , \widehat{\xi}_n))
$$
with the partition function
$$ 
    Q\left(\widehat{\xi}_1, ... , \widehat{\xi}_n\right) = \frac{1}{N!\Lambda^{3N}} \int dr^N e^{-\beta U(r^N)} \prod_{i=1}^n \delta(\xi_i(r^N) - \widehat{\xi}_i)
$$
and the collective variables
$$ 
   \xi_1(r^N), \xi_2(r^N), ... , \xi_n(r^N)
$$
where each one corresponds to a value $\xi_i$.
In this case the free energy can be computed with a histogramm by counting the occurrences where the delta function is 1 and then summing over that.

### How is the free energy connected to the probability density?
Because the free energy can be written as the expectation value of the delta function we can rewrite this in terms of the partition function 
$$ 
    Q\left(\widehat{\xi}\right) = \frac{1}{N!\Lambda^{3N}} \int dr^N e^{-\beta U(r^N)} \delta(\xi(r^N) - \widehat{\xi})
$$
then the free energy is
$$ 
    \frac{Q(\widehat{\xi})}{Q_{NVT}} = \frac{e^{-\beta F(\widehat{\xi})}}{e^{-\beta F_{NVT}}}.
$$
Expressing $Q{\widehat{\xi}}$ and using the properties of the logarithm this becomes
$$
    F(\widehat(\xi)) = -k_BT ln(f(\widehat{\xi})) + F_{NVT}
$$ 
again because we're only interested in energy differences we can ignore the last term.

