# Homogenization via unit cell analysis
## Description
The unit cell approach is an effective way to obtain the complex permeability of the composite materials, which can be used in the finite element (FE) analysis of electromagnetic devices. 
In this repository, we implemented the Cauer circuit via the Lancoz (CVL) method to obtain the complex permeability in the form of the continued fraction using FreeFEM.

|<img src="https://github.com/ShingoHiruma/unitcell_homogenization/assets/49121385/5f86d172-4bb5-477e-9c84-59bee0cdc60b" width="50%">|<img src="https://github.com/ShingoHiruma/unitcell_homogenization/assets/49121385/8ce54314-ab7d-4c9a-96c5-fad5dce33ffc" width="80%">|
|:---:|:---:|
|Homogenization of composite materials|Unit cell analysis to determine $\langle\dot\mu\rangle$|


## Features
- Obtaining the complex permeability in the form of a continued fraction
- Applicable to the round wire, rectangular conductor, and arbitrarily shaped conductor
- Plotting the complex permeability against the frequency

## Download
[FreeFEM](https://freefem.org/) needs to be installed as a preliminary preparation. After completing the installation, double-click the edp file to run it.

## Method
Let us consider the uniform time-harmonic external magnetic flux density $B_0$ interlinkage across the unit cell $\Omega$. The complex permeability $\langle\dot\mu\rangle$ of the unit cell can be evaluated using the following formula:
$$\langle\dot\mu\rangle=\frac{-j\omega\int_\Omega |B_0|^2dS}{-j\omega\int_\Omega \nu |\textbf{B}|^2 dS + \int_\Omega \sigma|\textbf{E}|dS}$$
where $j,\omega,\nu,\sigma$ are the imaginary unit, angular frequency, magnetic reluctivity, and the conductivity of the conductive material in the unit cell.

By using the finite element discretization, the governing equation and the complex permeability can be represented in the discretized forms as follows:
$$(K+sN)\textbf{x}=\textbf{b}B_0$$
$$\langle\dot\mu\rangle=\frac{\int_\Omega dS}{\textbf{c}^\top(K+sN)^{-1}\textbf{b}}$$
where
$$K_{ij}=\int_\Omega \nabla N_i\cdot\nu\nabla N_j d\Omega,$$
$$N_{ij}=\int_\Omega \sigma N_iN_jd\Omega,$$
$$(\textbf{c})_i=\nu w \int \frac{dN_i}{dx}d\Gamma $$
$w$ is the half-width of the unit cell, and $N_i$ is the interpolation function of the i-th node.

Applying the CVL method [1] to the transfer function of the denominator of the complex permeability, we obtain
$$\langle\dot\mu\rangle=\frac{1}{\frac{1}{\kappa_1}+\frac{1}{\frac{1}{j\omega\kappa_2} + \frac{1}{\frac{1}{\kappa_3}+\frac{1}{\ddots}}}}$$


## Parameters
You can change the geometry of the conductor and the size of the unit cell by editing the edp file.
```
// Parameters
real sigma = 5.76e7;
real mu = 4.0*pi/(1.0e7);
real j0 = sigma;
real width = 0.0001;
real k = 0.5;
real radius = width*k;
```
## Data
Results are saved in a CSV file. The values of each term of the continued fraction are given as float data in the CSV file. The following figure shows the frequency dependence of the relative complex permeability, which is calculated from the obtained values of the continued fraction.

| Values  |
| ------------- | 
| 1.00000000.E+00| 
| 8.88230863.E-09| 
| 2.89535137.E+00| 
| 3.82237771.E-10| 
| 1.28846204.E+01| 
| 5.37494620.E-11| 
| 3.52091220.E+01| 
| 1.30581154.E-11| 
| 7.47474910.E+01| 

## Figures
<img src="https://github.com/ShingoHiruma/unitcell_homogenization/assets/49121385/b679afd4-85b3-4516-89d9-af3cfd1565c0" width="50%">
<img src="https://github.com/ShingoHiruma/unitcell_homogenization/assets/49121385/2866f0eb-7e08-4078-8819-01044136c408" width="50%">

## Reference
[1] S. Hiruma and H. Igarashi, "Homogenization Method Based on Cauer Circuit via Unit Cell Approach," in IEEE Transactions on Magnetics, vol. 56, no. 2, pp. 1-5, Feb. 2020, Art no. 7505805, doi: [10.1109/TMAG.2019.2946402.](https://ieeexplore.ieee.org/document/8957112)
