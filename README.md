# RRAM Transient Simulation Framework: SET and RESET Processes with Nonlinear Heat Transport

## Overview

This repository presents a computational framework for the transient simulation of resistive random-access memories (RRAM), developed using **COMSOL Multiphysics, MATLAB LiveLink, and custom physics implemented through COMSOL Physics Builder**.

The central objective of this research is to describe the coupled electrical, thermal, and morphological processes governing the formation and rupture of nanoscale conductive filaments in resistive memories.

The framework incorporates nonlinear heat transport, providing an alternative to conventional Fourier-based models when describing the thermal inertia observed during filament evolution.

### New developments

The original implementation focused on the RESET process, particularly the dissolution and eventual rupture of conductive filaments under relatively slow voltage pulses.

**The new version extends the simulation framework in two important directions:**

1. **SET and RESET simulation:** The framework now supports both the formation and growth of conductive filaments (SET) and their dissolution and rupture (RESET).
2. **Fast transient simulation:** In addition to relatively slow voltage-pulse regimes, the new version can simulate fast transient processes, extending its applicability to shorter electrical and thermal timescales.

These developments broaden the scope of the original computational framework and allow the investigation of a wider range of resistive-switching phenomena.

It is important to distinguish these new capabilities from the results presented in the published paper. The article focuses specifically on RESET processes under relatively slow voltage pulses. The SET and fast-transient capabilities belong to subsequent developments of the simulation framework and are not covered by that publication.

---

## Published Research

The mathematical formulation and numerical methodology underlying the original RESET model have been published in the international scientific journal *Mathematics and Computers in Simulation*, published by Elsevier.

**Moreno, E., Barrera, D., Ibáñez, M. J., & Roldán, J. B. (2026).**

**A nonlinear mathematical model for the transient heat equation in resistive memories.**

*Mathematics and Computers in Simulation.*

DOI: https://doi.org/10.1016/j.matcom.2026.10.040

Accepted: October 28, 2026.

The article introduces a nonlinear constitutive formulation for heat transport, motivated by the Landauer framework for nanoscale transport phenomena.

The resulting mathematical model couples:

- Electrical conduction and charge conservation.
- Joule heating and nonlinear thermal transport.
- Temperature-dependent conductive-filament evolution.
- Arrhenius-type kinetics governing filament dissolution.
- Dynamic geometry reconstruction and adaptive remeshing.

The governing equations are implemented using the finite-element weak formulation within COMSOL Physics Builder.

MATLAB coordinates the transient calculations, updates the conductive-filament geometry, and manages the successive simulation intervals through LiveLink.

The published study demonstrates how nonlinear heat transport can contribute to explaining the thermal behavior of RRAM devices without relying exclusively on artificially modified material properties.

### Citation

```bibtex
@article{Moreno2026NonlinearRRAM,
  author  = {Moreno, E. and Barrera, D. and Ibanez, M. J. and Roldan, J. B.},
  title   = {A nonlinear mathematical model for the transient heat equation in resistive memories},
  journal = {Mathematics and Computers in Simulation},
  year    = {2026},
  doi     = {10.1016/j.matcom.2026.10.040},
  url     = {https://doi.org/10.1016/j.matcom.2026.10.040}
}
```

---

## Why This Work?

An essential aspect of resistive switching in RRAM devices is the thermal response of the conductive filament during voltage-pulse operation.

During RESET, the conductive filament progressively dissolves until the electrical connection between the electrodes is interrupted.

This process is strongly temperature-dependent.

When the applied voltage decreases, the filament does not necessarily cool at the same rate as the electrical excitation. Instead, its temperature can exhibit a delayed response, remaining elevated after the voltage has started to decrease.

This phenomenon is commonly described as thermal inertia or thermal lag.

The persistence of elevated temperatures is particularly important because conductive-filament dissolution follows an Arrhenius-type dependence:

$$
\frac{\partial r}{\partial t}
=
-A\exp\left(-\frac{E_a}{k_B T}\right)
$$

where:

- \(r\) is the local conductive-filament radius.
- \(A\) is the kinetic prefactor.
- \(E_a\) is the activation energy.
- \(k_B\) is Boltzmann's constant.
- \(T\) is the local temperature.

Because of the exponential temperature dependence, even relatively small differences in the thermal response can produce substantial changes in filament dissolution rates.

Consequently, thermal inertia can significantly influence the evolution of the filament and the switching characteristics of the device.

### Limitations of conventional thermal models

In conventional electrothermal simulations, heat conduction is generally described using Fourier's law:

$$
\mathbf{q}=-\boldsymbol{\kappa}_0\nabla T
$$

where $\mathbf{q}\) is the heat-flux vector and \(\boldsymbol{\kappa}_0$ is the thermal-conductivity tensor.

Although this formulation is appropriate for many macroscopic applications, its direct application to nanoscale conductive filaments may not adequately reproduce all the thermal behavior observed experimentally.

In particular, reproducing certain RESET characteristics using conventional models has sometimes required artificially increasing the density or specific heat capacity of the simulated materials.

Such adjustments can improve agreement with experimental curves but may lead to effective material parameters that are difficult to justify physically.

### Nonlinear heat transport

Our approach introduces nonlinear contributions to the heat flux:

$$
\mathbf{q}_{\mathrm{total}}
=
\mathbf{q}_{\mathrm{linear}}
+
\mathbf{q}_{\mathrm{nonlinear}}
$$

The nonlinear contribution depends on higher-order terms involving the temperature gradient.

This modification provides additional flexibility for describing heat transport at the nanoscale and can produce thermal responses that differ substantially from those predicted by the conventional linear Fourier model.

The resulting thermal behavior influences the Arrhenius kinetics of filament dissolution and, consequently, the electrical response during RESET.

The purpose is not simply to reproduce experimental curves, but to investigate a physically motivated mathematical description of the coupled electrothermal processes.

Nonlinear thermal transport is proposed as a mechanism contributing to the observed behavior, rather than being asserted as the only possible explanation of thermal inertia.

**Explanatory video:**

https://drive.upm.es/s/gG7RfgdbLpwyNDK

---

## From RESET-Only Simulation to SET and RESET

The original computational implementation was designed primarily to reproduce the progressive destruction of conductive filaments during RESET.

The updated framework extends this approach to both switching directions.

### RESET: Filament dissolution and rupture

During RESET, the conductive filament progressively decreases in cross-sectional area as a result of temperature-dependent material migration.

The simulation tracks the electrical and thermal response while updating the filament geometry.

The process continues until the filament reaches a rupture condition and the device transitions toward its high-resistance state (HRS).

The published article concentrates on this process.

### SET: Filament formation and growth

During SET, the conductive pathway develops or grows through the dielectric material, allowing the device to transition from a high-resistance state toward a low-resistance state (LRS).

The new version of the simulation framework extends the numerical treatment to this process.

The objective is to describe filament formation and growth while accounting for the interaction between the electrical excitation, temperature distribution, and evolving conductive geometry.

SET and RESET involve different morphological evolution processes. Consequently, the growth kinetics used for SET should not be assumed to be identical to the dissolution law employed in the published RESET model.

### Fast transient simulation

Another important extension concerns the temporal resolution and operating regime of the simulations.

The original published work concentrates on RESET processes under relatively slow voltage pulses.

The new version can also address fast transient phenomena, in which the electrical excitation and thermal response evolve over substantially shorter timescales.

This capability is particularly relevant for investigating the dynamic behavior of resistive memories under rapid switching conditions.

The extension to fast transients broadens the range of operating conditions that can be studied, although the quantitative validity of the physical assumptions and numerical approximations must be assessed for the corresponding timescales.

### Scope of the different versions

| Feature | Published 2026 Model | New Version |
|---|---|---|
| RESET simulation | Yes | Yes |
| SET simulation | Not addressed | Yes |
| Nonlinear thermal transport | Yes | Extended framework |
| Relatively slow voltage pulses | Yes | Yes |
| Fast transient simulation | Not addressed | Yes |
| Electrical and thermal coupling | Yes | Yes |
| Conductive-filament evolution | Dissolution | Growth and dissolution |
| MATLAB–COMSOL framework | Yes | Yes |

The new capabilities described here correspond to software development beyond the scope of the published article.

---

## The Repository

Repository:

https://github.com/maxwellfree/RRAM-models-with-COMSOL6.0-new-physics-

The repository provides computational resources for studying transient electrothermal phenomena in resistive memories.

The original RESET implementation includes the following components:

**connect.m**

A MATLAB script that establishes communication between MATLAB and the COMSOL Multiphysics server through LiveLink.

**FindResetTrans.m**

A MATLAB script for running the transient RESET simulation, tracking the applied voltage, electrical current, temperature evolution, and conductive-filament dissolution.

**Ni-HfO2-Si.mph**

A COMSOL model containing the device geometry and the physical configuration used in the original simulation framework.

**RRAMNonLinear6_2.mphphb**

A custom COMSOL Physics Builder file implementing the nonlinear heat-transport formulation.

Together, these components establish the original numerical environment for studying the transient RESET process.

The newer SET and fast-transient developments extend this framework. The original file descriptions above should not be interpreted as a complete inventory of the newer implementation.

---

## Numerical Methodology

The computational approach combines finite-element analysis with sequential updates of the conductive-filament geometry.

The simulation involves three strongly coupled physical processes.

### 1. Electrical problem

The electrical potential is calculated by solving the governing equations for charge conservation and electrical transport.

The resulting electric field determines the current distribution and Joule-heating source.

### 2. Thermal problem

The temperature distribution is calculated using the heat equation, including nonlinear contributions to the thermal flux.

The thermal model accounts for the energy generated by electrical conduction and the redistribution of heat through the device.

### 3. Conductive-filament evolution

The filament geometry evolves according to temperature-dependent kinetic laws.

During RESET, the model describes filament dissolution.

In the extended SET framework, filament growth is also considered.

### Sequential simulation procedure

The transient calculation is divided into successive time intervals.

Within each interval:

1. MATLAB coordinates the COMSOL simulation.
2. COMSOL calculates the electrical and thermal fields for the current device geometry.
3. The temperature distribution is used to evaluate filament-evolution kinetics.
4. MATLAB updates the conductive-filament geometry.
5. The computational domains and finite-element mesh are reconstructed.
6. The next simulation interval begins using the updated configuration.

This procedure allows the evolving geometry to interact with the electrical and thermal fields throughout the transient simulation.

In the published RESET implementation, the electrothermal equations are solved together for a fixed geometry within each interval, while morphological changes are incorporated sequentially between intervals.

---

## MATLAB + COMSOL Video

A walkthrough video demonstrates how to perform transient RESET simulations using MATLAB and COMSOL Multiphysics through LiveLink.

The tutorial shows how MATLAB repeatedly calls the COMSOL model, updates simulation parameters, modifies the conductive-filament geometry, and records the evolution of the relevant physical variables.

A train of voltage pulses is divided into shorter time intervals, allowing the filament geometry to evolve progressively during the simulation.

At each stage, the electrical and thermal fields are recalculated for the updated geometry.

This procedure provides a practical example of automating multiphysics simulations involving changing computational domains.

**MATLAB simulation video:**

https://drive.upm.es/s/LbDB6RLMEyDN2pM

**RESET verification video:**

https://drive.upm.es/s/9W3CjiXP8B4fojg

---

## Mathematical Formulation

The mathematical formulation is implemented using the finite-element weak formulation.

This approach provides the flexibility required to introduce physical equations that are not directly available in the standard COMSOL physics interfaces.

The tutorial explains how the governing differential equations are transformed into their weak forms and subsequently implemented using COMSOL Physics Builder.

Particular attention is given to the relationship between conventional finite-element notation and the expressions required by the software.

The treatment of Dirichlet and Neumann boundary conditions is also discussed.

**Weak formulation video:**

https://drive.upm.es/s/9kEmDfLS99fx5r4

---

## COMSOL Physics Builder

COMSOL Physics Builder allows researchers to create custom physics interfaces by defining governing equations, dependent variables, material properties, and boundary conditions.

In this project, Physics Builder is used to implement the nonlinear thermal formulation developed for the simulation of resistive memories.

The tutorial explains how the weak formulation is translated into the corresponding COMSOL expressions and how the resulting custom physics can be incorporated into a simulation model.

**COMSOL Physics Builder video:**

https://drive.upm.es/s/em6rHxcLWy7n8sk

---

## COMSOL Model Using the New Physics

This tutorial presents the construction of the COMSOL model using the custom physics developed through Physics Builder.

The video explains the main steps required to define the model, incorporate the new equations, and prepare the numerical simulation.

It provides a practical demonstration of how the mathematical formulation can be integrated into a working multiphysics environment.

**COMSOL model video:**

https://drive.upm.es/s/Eqatgf8FSsN5MgF

---

## Research Perspectives

The development of a unified simulation framework for SET and RESET processes opens several research directions.

These include investigating the influence of nonlinear thermal transport on filament formation and rupture, studying the relationship between pulse duration and switching dynamics, and examining the effects of thermal inertia across different operating regimes.

The extension to fast transients also provides opportunities to investigate shorter switching timescales and the limitations of conventional electrothermal descriptions.

Future studies may compare the different formulations against experimental measurements and examine their predictive capabilities for different materials, geometries, and electrical excitation conditions.

The broader objective is to develop physically consistent and computationally reproducible tools for investigating resistive-switching devices.

---

## Contact

For questions regarding the mathematical formulation, COMSOL Physics Builder implementation, MATLAB LiveLink procedures, or the newer SET and fast-transient simulation developments, please contact:

**E. Moreno**

Universidad Politécnica de Madrid

Email: [em.moreno@upm.es](mailto:em.moreno@upm.es)

I will be glad to provide further information or clarification concerning the use, development, and application of these research tools.
