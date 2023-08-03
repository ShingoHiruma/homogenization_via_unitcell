# unitcell_homogenization
## Description
The unit cell approach is an effective way to obtain the complex permeability of the composite materials, which can be used in the finite element (FE) analysis of electromagnetic devices. 
In this repository, we implemented the Cauer circuit via the Lancoz (CVL) method to obtain the complex permeability in the form of the continued fraction using FreeFEM.

## Features
We have implemented the following cases.
- Round wire
- Rectangular conductor

## Physics
Let us consider the uniform time-harmonic external magnetic flux density $B_0$ interlinkage across the unit cell $\Omega$. The complex permeability $\langle\dot\mu\rangle$ of the unit cell can be evaluated using the following formula:
$$\langle\dot\mu\rangle=\frac{-j\omega\int_\Omega |B_0|^2dS}{-j\omega\int_\Omega \nu |\textbf{B}|^2 dS + \int_\Omega \sigma|\textbf{E}|dS}$$
where $j,\omega,\nu,\sigma$ are the imaginary unit, angular frequency, magnetic reluctivity, and the conductivity of the conductive material in the unit cell.

Using the Galerkin method, the governing equation and the complex permeability can be represented in the discretized forms as follows:
$$(K+sN)\textbf{x}=\textbf{b}B_0$$
$$\langle\dot\mu\rangle=\frac{\int_\Omega dS}{\textbf{c}^\top(K+sN)^{-1}\textbf{b}}$$
where
$$K=\int_\Omega \nabla N_i\cdot\nu\nabla N_j d\Omega,$$
$$N=\int_\Omega \sigma N_iN_jd\Omega,$$
$$(\textbf{c})_i=\nu w \int \frac{dN_i}{dx}d\Gamma $$
where w is the half-width of the unit cell, and $N_i$ is the interpolation function of the i-th node.

Applying the CVL method to the transfer function at the denominator of the complex permeability, we obtain
$$\langle\dot\mu\rangle=\frac{1}{\frac{1}{\kappa_1}+\frac{1}{\frac{1}{j\omega\kappa_2} + \frac{1}{\frac{1}{\kappa_3}+\frac{1}{\ddots}}}}$$
## Download
The programs (.edp) can be run on FreeFEM. 
