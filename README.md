# unitcell_homogenization
## Description
The unit cell approach is an effective way to obtain the complex permeability of the composite materials, which can be used in the finite element (FE) analysis of electromagnetic devices. 
In this repository, we implemented the Cauer circuit via the Lancoz (CVL) method to obtain the complex permeability in the form of the continued fraction using FreeFEM.

## Features
We have implemented the following cases.
- Round wire
- Rectangular conductor

## Mathematics
Let us consider the uniform time-harmonic external magnetic flux density $$B_0$$ interlinkage across the unit cell $$\Omega$$. The complex permeability $$\langle\dot\mu\rangle$$ of the unit cell can be evaluated using
$$\langle\dot\mu\rangle=\frac{-j\omega\int_\Omega |B_0|^2dS}{-j\omega\int_\Omega \nu |\textbf{B}|^2 dS + \int_\Omega \sigma|\textbf{E}|dS}$$
where 

## Download
The programs (.edp) can be run on FreeFEM. 
