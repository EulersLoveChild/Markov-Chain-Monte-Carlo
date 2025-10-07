# Markov Chain Monte Carlo

In the code, we use the Monte Carlo Markov Chain numerical method, thoroughly described in [this paper](https://arxiv.org/pdf/hep-lat/0702020), to numerically verify approximations in lattice field theory equations. Namely, the 1-pt functions $\langle x_i\rangle$ and 2-pt functions $\langle x_i x_j \rangle$ of a lattice field theory can be written as an infinite hierarchy of equations in terms of higher powers of the perturbation constant $N^{-1/2}$. Professor Tom Banks [conjectured](https://arxiv.org/pdf/2003.13136) that ignoring terms of order $N^{-3/2}$ and lower will still satisfy these equations to a high degree. In our [manuscript](https://arxiv.org/pdf/2509.08501), which can be found here, we tested this claim for a simple toy model on a $2 \times 2$ and $3 \times 3$ lattice. We found a strong match, which suggests his claim is accurate.

The specific method that we used was the Markov Chain Monte Carlo method, which allows us to solve ratios of integrals - terms that often appear in Quantum Field Theory. However, both diverge, so direct calculation is not possible. The general outline of the algorithm is as follows:
1. We update all sites until their values 'hover' over the mean.
2. We begin taking measurements using the thermalized values. At the start of this phase, we calculate the autocorrelation $\rho$.
3. After obtaining many measurements, we take a subset of these as our Markov Chain based on our calculation for $\rho$.

The exact specifications for this code are:
- $N_{therm}$, the number of sweeps of each site in the thermalization phase, is $10^3$
- $\rho$, the autocorrelation, was measured after $10^4$ sweeps. The number of measurements that were to be skipped to build the Markov Chain was chosen based on when $\rho \leq 0.1$.
- $N_{measure}$, the number of sweeps per site in the measurement phase, was taken to be $2 \times 10^5$.
- $2\Delta$, the size of the interval for updating each site, is taken to be $3.50$.

More information on the specifications, including the choice of the discrete Laplacian for the lattice, can be found [here](https://arxiv.org/pdf/2509.08501).
