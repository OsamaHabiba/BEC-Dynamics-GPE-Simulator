# BEC Dynamics Simulator

A Python-based numerical solver for the **Gross-Pitaevskii Equation (GPE)**, used to study the dynamics of **Bose-Einstein Condensates (BEC)**. This implementation utilizes a modified **Visscher's Method** to propagate the wavefunction in real time.

## Theoretical Background

The Gross-Pitaevskii Equation (GPE) is a cubic nonlinear Schrödinger equation (NLSE) that describes the dynamics of a weakly-interacting BEC at zero temperature ($T=0$):

$$i\hbar\frac{\partial}{\partial t}\psi(\mathbf{r}, t) = \left[ -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r}) + g|\psi(\mathbf{r}, t)|^2 \right]\psi(\mathbf{r}, t)$$

Where:
- $\psi(\mathbf{r}, t)$ is the macroscopic wavefunction.
- $V(\mathbf{r})$ is the external trapping potential (e.g., harmonic trap).
- $g$ is the interaction constant, related to the s-wave scattering length $a_s$ by $g = \frac{4\pi a_s \hbar^2}{m^*}$.

### Dimensionless Formulation
For numerical stability, the code uses a dimensionless form of the GPE:

$$i\frac{\partial}{\partial t}\psi = \left[ -\frac{1}{2}\nabla^2 + V(x, y) + \eta|\psi|^2 \right]\psi$$

Where $\eta$ represents the nonlinearity (repulsive for $\eta > 0$, attractive for $\eta < 0$).

## Numerical Method: Visscher's Scheme

The simulator implements **Visscher's Method**, which uses a staggered-time approach to evolve the real ($R$) and imaginary ($I$) parts of the wavefunction:

1. **Staggered Time Steps**: $R$ is defined at integer steps ($t$), and $I$ at half-integer steps ($t + \frac{\Delta t}{2}$).
2. **Explicit Update Rules**:
   $$R(t + \frac{\Delta t}{2}) = \frac{R(t - \frac{\Delta t}{2}) + \Delta t [-\frac{1}{2}\nabla^2 + V + \eta I(t)^2] I(t)}{1 - \Delta t \eta R(t - \frac{\Delta t}{2}) I(t)}$$
   $$I(t + \frac{\Delta t}{2}) = \frac{I(t - \frac{\Delta t}{2}) - \Delta t [-\frac{1}{2}\nabla^2 + V + \eta R(t)^2] R(t)}{1 + \Delta t \eta I(t - \frac{\Delta t}{2}) R(t)}$$

This scheme provides a fast and simple update rule while maintaining stability by choosing $\Delta t < \frac{\Delta x^2}{4}$.

## Features

- **2D/Quasi-2D Simulations**: Support for isotropic and anisotropic elliptical harmonic traps.
- **Nonlinear Phenomena**: Capability to simulate:
    - **Vortex Formation**: Nucleation of quantized vortices via laser stirring.
    - **Soliton Propagation**: Dark and bright solitons in confined geometries.
    - **Sound Propagation**: Density perturbations and sound wave dynamics.
- **Custom Observers**: Modular system to track and record energy, density, and wavefunction norms during evolution.


