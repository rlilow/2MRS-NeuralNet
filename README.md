# 2MRS-NeuralNet

Neural network reconstruction of density and velocity fields from the 2MASS Redshift Survey

### Description

This repository provides the 3D matter density and peculiar velocity fields reconstructed from 2MRS using a neural network, described in

> Robert Lilow, Punyakoti Ganeschaiah Veena & Adi Nusser, [arXiv:2404.?????](https://arxiv.org/abs/2404.?????).

## Data

The reconstructed matter density, $1+\delta$, and peculiar velocity components relative to the CMB, $v_x, v_y, v_z$, smoothed with a Gaussian window of width $3 \, h^{-1} \, \mathrm{Mpc}$, as well as their estimated errors, are available for download from this [Dropbox folder](https://www.dropbox.com/scl/fo/wb8iyg113hyin4ni7srkg/h?rlkey=5k0vcyhgi9vbtrkpwl206d6u6&dl=0).

They can be loaded in Python via

```python
import numpy as np

density = np.load("density.npy")
xVelocity = np.load("xVelocity.npy")
yVelocity = np.load("yVelocity.npy")
zVelocity = np.load("zVelocity.npy")

density_error = np.load("density_error.npy")
xVelocity_error = np.load("xVelocity_error.npy")
yVelocity_error = np.load("yVelocity_error.npy")
zVelocity_error = np.load("zVelocity_error.npy")
```

They are discretized on a regular regular cubic grid of size $128\times128\times128$ of side length $400 \, h^{-1} \, \mathrm{Mpc}$ in comoving Galactic coordinates.
The coordinates of the grid cell centers are each running from $-198.4375 \, h^{-1} \, \mathrm{Mpc}$ to $+198.4375 \, h^{-1} \, \mathrm{Mpc}$ in steps of $3.125 \, h^{-1} \, \mathrm{Mpc}$.
Thus, the field values at the numpy array indices [i, j, k] correspond to the Galactic coordinates

> $\mathrm{GX}_i = (i - 63.5) \; 3.125 \, h^{-1} \, \mathrm{Mpc} \quad  \mathrm{for} \quad 0 \leq i \leq 127$
> 
> $\mathrm{GX}_j = (j - 63.5) \; 3.125 \, h^{-1} \, \mathrm{Mpc} \quad  \mathrm{for} \quad 0 \leq j \leq 127$
> 
> $\mathrm{GX}_k = (k - 63.5) \; 3.125 \, h^{-1} \, \mathrm{Mpc} \quad  \mathrm{for} \quad 0 \leq k \leq 127$

However, only field values within a sphere of radius $200 \, h^{-1} \, \mathrm{Mpc}$ are valid. Values outside this sphere are set to `NaN`.