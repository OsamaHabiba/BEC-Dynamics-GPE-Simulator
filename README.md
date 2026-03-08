# BEC-Dynamics-GPE-Simulator
(A Numerical Study on the Dynamics of Bose-Einstein Condensates using the Gross-Pitaevskii Equation
# BEC Dynamics Simulator

[cite_start]A Python-based numerical solver for the **Gross-Pitaevskii Equation (GPE)**, used to study the dynamics of **Bose-Einstein Condensates (BEC)**[cite: 1, 13]. [cite_start]This implementation utilizes a modified **Visscher's Method** to propagate the wavefunction in real time[cite: 16].

## Theoretical Background

[cite_start]The Gross-Pitaevskii Equation (GPE) is a cubic nonlinear Schrödinger equation (NLSE) that describes the dynamics of a weakly-interacting BEC at zero temperature ($T=0$)[cite: 88, 95]:

$$i\hbar\frac{\partial}{\partial t}\psi(\mathbf{r}, t) = \left[ -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r}) + g|\psi(\mathbf{r}, t)|^2 \right]\psi(\mathbf{r}, t)$$

Where:
- [cite_start]$\psi(\mathbf{r}, t)$ is the macroscopic wavefunction[cite: 110].
- [cite_start]$V(\mathbf{r})$ is the external trapping potential (e.g., harmonic trap)[cite: 108].
- [cite_start]$g$ is the interaction constant, related to the s-wave scattering length $a_s$ by $g = \frac{4\pi a_s \hbar^2}{m^*}$[cite: 91].

### Dimensionless Formulation
[cite_start]For numerical stability, the code uses a dimensionless form of the GPE[cite: 107, 108]:

$$i\frac{\partial}{\partial t}\psi = \left[ -\frac{1}{2}\nabla^2 + V(x, y) + \eta|\psi|^2 \right]\psi$$

[cite_start]Where $\eta$ represents the nonlinearity (repulsive for $\eta > 0$, attractive for $\eta < 0$)[cite: 109].

## Numerical Method: Visscher's Scheme

[cite_start]The simulator implements **Visscher's Method**, which uses a staggered-time approach to evolve the real ($R$) and imaginary ($I$) parts of the wavefunction[cite: 267, 269]:

1. [cite_start]**Staggered Time Steps**: $R$ is defined at integer steps ($t$), and $I$ at half-integer steps ($t + \frac{\Delta t}{2}$)[cite: 269].
2. **Explicit Update Rules**:
   $$R(t + \frac{\Delta t}{2}) = \frac{R(t - \frac{\Delta t}{2}) + \Delta t [-\frac{1}{2}\nabla^2 + V + \eta I(t)^2] I(t)}{1 - \Delta t \eta R(t - \frac{\Delta t}{2}) I(t)}$$
   $$I(t + \frac{\Delta t}{2}) = \frac{I(t - \frac{\Delta t}{2}) - \Delta t [-\frac{1}{2}\nabla^2 + V + \eta R(t)^2] R(t)}{1 + \Delta t \eta I(t - \frac{\Delta t}{2}) R(t)}$$

[cite_start]This scheme provides a fast and simple update rule while maintaining stability by choosing $\Delta t < \frac{\Delta x^2}{4}$[cite: 266, 278].

## Features

- [cite_start]**2D/Quasi-2D Simulations**: Support for isotropic and anisotropic elliptical harmonic traps[cite: 113, 222, 223].
- **Nonlinear Phenomena**: Capability to simulate:
    - [cite_start]**Vortex Formation**: Nucleation of quantized vortices via laser stirring[cite: 122, 127].
    - [cite_start]**Soliton Propagation**: Dark and bright solitons in confined geometries[cite: 134, 137].
    - [cite_start]**Sound Propagation**: Density perturbations and sound wave dynamics[cite: 373].
- **Custom Observers**: Modular system to track and record energy, density, and wavefunction norms during evolution.

## Installation

Ensure you have the following dependencies:
- Python 3.x
- NumPy
- SciPy
- Matplotlib

```bash
pip install numpy scipy matplotlib
