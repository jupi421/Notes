Status: #LectureNote
Tags: [[Advanced_molecular_simulation]]

# AMSLecture1-Introduction and Statisticsw

### Why are free energies fundametally important?
The [[Zettelkasten/Free energies|free energies]] is the determining factor for:
- Phase behavior such as the coexistence of two or more phases. The free energy at coexistence lines in phase diagrams has to be equal
- Phase transitions
- Hydrophobic effects
- Ionic association and dissociation
- Protein folding
- Solvation
- Membrane transport

###  Why does the Boltzmann Factor hold in equilibrium but not in non equilibrium cases? 
The Boltzmann factor represents the probability to find the system in a state of a given energy E. It relies on the assumption of a stable temperature throughout the system, which is given in equilibrium. As the energy for non equilibrium states is much higher than for equilibrium states the probability given by the Boltzmann factor is very low as it favours minimal energy configurations and thus is not applicable to describe not equilibrated systems.

### What is the cumulative probability distribution?
[[Zettelkasten/Cumulative_Probability_Distribution|Cumulative Probability Distribution]]

### What are the different statistical moments and what do they say about the system?
[[Zettelkasten/Statistical_Moments|Statistical Moments]] ... 

### What is the purpose of the | term | in $f_Y(y)$?
The term on the left-hand side in ^pdf-compression
$$ 
    f_Y(y) = f_X(x) \left| \frac{dy}{dx} \right|^{-1}
$$ 
accounts for the compression/inflation of the PDF when being mapped from x to y. If $g(x)$ has a steep slope, then the interval in x gets mapped onto a larger interval in y. Hence the probability density in y decreases.
