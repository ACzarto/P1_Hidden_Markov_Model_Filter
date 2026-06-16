# P1_Hidden_Markov_Model_Filter
This project implements the Hidden Markov Model Filter (or Grid Filter) and compares the results of this Bayesian algorithm with the maximum likelihood approach (which does not consider a priori information about the source).

In this algorithm, we have an information source that emits symbols from a discrete alphabet, where the possible outcomes are

$$\mathcal{A} = \[S_1, S_2, S_3, \dots, S_q\]$$

This filter assumes that we have full a priori knowledge of the system's statistics, specifically:
1. The **Transition Probability Matrix** ($\Pi$), which defines how the hidden states evolve over time.
2. The **Initial State Probability Vector** ($p_0$), representing the prior belief of the starting state.
3. The **Observation Model** ($\beta_n$), which maps the relationship between the hidden states and the noisy measurements.

The algorithm evaluates the state estimation performance across different noise levels by varying the noise standard deviation $\sigma_W$. 

### Mathematical Model

The discrete-time state transitions are governed by the transition matrix $\Pi$, where the prior probability is updated at each step $n$ as

$$p_{n|n-1} = \Pi \cdot p_{n-1|n-1}$$

The update step incorporates the emission probabilities function $\beta_n$ (the observation model) under an Additive White Gaussian Noise (AWGN) assumption and the measurements $Y_n$

$$\beta_n = \frac{1}{\sqrt{2\pi\sigma_W^2}} \exp\left( -\frac{(Y_n - \mathcal{A})^2}{2\sigma_W^2} \right)$$

After computing the element-wise multiplication between the prediction and the observation likelihood, the posterior probability vector $p_{n|n}$ is normalized

$$p_{n|n} = \frac{\beta_n \odot p_{n|n-1}}{\sum (\beta_n \odot p_{n|n-1})}$$

Finally, the symbol estimation is performed using the Maximum A Posteriori (MAP) criterion:

$$\hat{S}_{n|n} = \arg\max_{S_k \in \mathcal{A}} (p_{n|n}[k])$$
