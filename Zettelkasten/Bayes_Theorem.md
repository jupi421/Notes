Topic: [[Statistics_and_Probabilities]]

# Bayes' theorem

Bayes theorem allows to calculate a probability of an event $A$ considering new or more information (condition $B$) that may be relevant to the event.

It is derived from the definition of conditional probabilities 
$$
\begin{aligned}
    f(a|b) = \frac{f(a, b)}{f_B(b)}\\
    f(b|a) = \frac{f(b, a)}{f_A(a)}
\end{aligned}
$$
When expressing the joint probability distribution for both PDF's and setting them equal we can write the Bayes theorem as
$$ 
    f(a|b) = \frac{f(b|a)f_A(a)}{f_B(b)}
$$
Here the PDF $f(a|b)$ is the posterior PDF that we want to compute with the new information, and $f(a)$ is the prior PDF.

Integrating results in the conditional probability.
