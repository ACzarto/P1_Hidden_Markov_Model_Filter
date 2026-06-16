# P1_Hidden_Markov_Model_Filter
This project implements the Hidden Markov Model Filter (or Grid Filter) and compares the results of this Bayesian algorithm with the maximum likelihood approach (which does not consider a priori information about the source).

The algorithm evaluates the state estimation performance across different noise levels by varying the standard deviation $\sigma_W$. 

### Mathematical Model

The discrete-time state transitions are governed by the transition matrix $A$, where the prior probability is updated at each step $n$ as

$$p_{n|n-1} = A \cdot p_{n-1|n-1}$$.

The update step incorporates the emission probabilities function $\beta_n$ (the observation model) under an Additive White Gaussian Noise (AWGN) assumption:

$$\beta = \frac{1}{\sqrt{2\pi\sigma_W^2}} \exp\left( -\frac{(Y_n - \text{alphabet})^2}{2\sigma_W^2} \right)$$
