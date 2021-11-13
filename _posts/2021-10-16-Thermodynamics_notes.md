---
layout: default
title:  "Thermodynamics notes"
date:   2021-10-16 15:03:39 +0800
categories: Physics

---

# Background

There are a lot of books on thermodynamics and thermostatistics, but Herbert B Callen's *Thermodynamics and an introduction to Thermostatistics* show an especially beautiful and unconventional structure.

For statistical mechanics we refer to Zonghan Lin's book.

# Basic Postulates for Thermodynamics

Herbert uses four postulates to replace traditional laws of thermodynamics.

1. There exist particular states (called equilibrium states) of simple systems that, macroscopically, are characterized completely by the internal energy U, the volume V, and the mole numbers N1, N2, ..., N, of the chemical components.
2. There exists a function ( called the entropy S) of the extensive parameters of any composite system, defined for all equilibrium states and the values assumed by the extensive parameters in the absence of an internal constraint are those that maximize the entropy over the manifold of constrained equilibrium states.
3. The entropy of a composite system is additive over the constituent subsystems. The entropy is continuous and differentiable and is a monotonically increasing function of the energy.
4. The entropy of any system vanishes in the state for which $\frac{\part U}{\part S} = 0$

There are no such thing as the second law of the thermodynamics since it has been contained in the P2, and third law in P4. 

Herbert then defined thermodynamics intensity variables using P1 and P3:
$$
U = U(S,V,N_1,\dots,N_n) \\
\frac{\part U}{\part S } = T,temperature\\
\frac{\part U}{\part V} = -P,pressure\\
\frac{\part U}{\part N_i} =\mu_i,chemical\quad potential \\
dQ = TdS,quasi-static\quad heat-flux \\
$$
Using the P1, P2 and energy conservation(not contained in the postulates), we get equilibrium condition for thermal, mechanical, matter flow, chemical equilibrium.

Define physical properties 
$$
\text{coefficient of thermal expansion}: \alpha = \frac{1}{V}(\frac{\part V}{\part T})_{P} \\
\text{isothermal compressibility}: \kappa_T = -\frac{1}{V}(\frac{\part V}{\part P})_{T} \\
\text{molar heat capacity at constant pressure}: c_p = \frac{1}{N}(\frac{dQ}{dT})_P
$$


# Formal relationship

## Gibbs-Duhem relation

Using Euler equation of S, the intensity variables are not independent, for single component 
$$
SdT-VdP+d\mu = 0
$$

Actually chemicl potential is exactly the molar Gibbs function

## The energy minimum principle

Using implicit function we can prove that the equilibrium value of energy at a given entropy is the minimum.

## Legendre Transformations and thermodynamic potential

Legendre transformation's meaning is to transform the independent variable in formal structure from extensive variables to intensive variables. We have
$$
F = U[T] = U-TS,Helmholtz \\
H = U[P] = U + PV, enthalpy \\
G = U[T,P] = U-TS+PV,Gibbs
$$
These thermodynamic potentials all reach their minimum value when connected to its Legendre transformation variable sources. 

- Helmholtz free energy: available work at constant temperature, the decrease in Helmholtz free energy equals the work delivered.
- Enthalpy: heat added to a system at constant pressure， Joule-Thomson process

## Maxwell Relation

The relation between four thermodynamical potentials: U,F,G,H three extensive variables: V,N,S, three intensive variables: $\mu$,T,P is called Maxwell relationship. Maxwell relationship consists of two parts: differential relationship and partial derivative commutability.

Maxwell relation is used in **Reduction of derivatives**. What we mean by reduction of derivatives is to transform the form $\frac{\part X}{\part Y}$ into the expressions constructed by three physical properties, where X,Y are two arbitrary thermodynamic variables.

To see why this is reasonable, we show that three phsical properties are equivalent with the fundamental equation. 
$$
\frac{\part^2g}{\part T^2} = -\frac{c_p}{T} \\
\frac{\part^2g}{\part P^2} = v\kappa_T \\
\frac{\part^2 g}{\part T\part P} =v\alpha  \\
$$
so we can get Gibbs form from the physical property, and use Legendre transformation we can get the fundamental equation.



# Stability

The real thermodynamics state lies where entropy is maximum, this is actully a desciprtion for stability. The basic requirement for stability of S is 
$$
(\frac{\part^2 S}{\part U^2})_V \leq 0\\
(\frac{\part^2 S}{\part V^2})_U \leq 0\\
(\frac{\part^2 S}{\part U^2})_V (\frac{\part^2 S}{\part V^2})_U-(\frac{\part^2 S}{\part V \part U}) \geq 0\\
$$
This requires the tangent plane of S with U and V are always under S.

By Legendre transformation, convexity in F, H, G can be get, too. In gerneral, for a potential 

Use reduction, the phsical consequences are 
$$
c_v \geq 0\\
\kappa_T \geq 0\\
$$




# First order phase transition

 Phase transition is caused by the hidden instable state. For first order phase transition, multiple local state states exist with different Gibbs function value, so the actual state depends on which state is the most stable. When first-order phase transition happens, the molar Gibbs function remains equal, while other potential may be discontinuous, which defines the first-oreder transition. The discontinuity in molar entropy causes the **latent heat**
$$
l = T\Delta S = \Delta h
$$

## Clapeyron Equation

P-T diagram reflects the change in molar volume
$$
\frac{dP}{dT} = \frac{l}{T\Delta v}
$$

## P-v diagram

There are several important diagrams for comprehension of first-order transition:

<img src="2021-10-16-Thermodynamics_notes.assets/Screen Shot 2021-10-30 at 11.51.13 AM.png" alt="Screen Shot 2021-10-30 at 11.51.13 AM" style="zoom:25%;" />

<img src="2021-10-16-Thermodynamics_notes.assets/Screen Shot 2021-10-30 at 11.51.44 AM.png" alt="Screen Shot 2021-10-30 at 11.51.44 AM" style="zoom:25%;" />

<img src="2021-10-16-Thermodynamics_notes.assets/Screen Shot 2021-10-30 at 11.52.12 AM.png" alt="Screen Shot 2021-10-30 at 11.52.12 AM" style="zoom:33%;" />

<img src="2021-10-16-Thermodynamics_notes.assets/Screen Shot 2021-10-30 at 11.53.20 AM.png" alt="Screen Shot 2021-10-30 at 11.53.20 AM" style="zoom:50%;" />

From the last graph the discontinuty of molar volume is displayed.

<img src="../../Library/Application Support/typora-user-images/Screen Shot 2021-10-30 at 11.58.55 AM.png" alt="Screen Shot 2021-10-30 at 11.58.55 AM" style="zoom:33%;" />

## Composite system

Why there is just one triple point in p-T diagram for water rather than many? **Gibbs phase rule** constrains the possibility of phases for us:

For a system with r components, write
$$
u = u(s,v,x_1,\dots,x_{r-1}) \\
$$
where $x_i$ is the mole fractions. We discuss a simple system with 2 components and 3 phases, equations are: 
$$
\mu_1^1(T,P,x_1^1) = \mu_1^2(T,P,x_1^2) = \mu_1^3(T,P,x_1^3)  \\
\mu_2^2(T,P,x_1^1) = \mu_2^2(T,P,x_1^2) = \mu_2^3(T,P,x_1^3)  \\
$$
There are 4 equations and 5 variables($T, P, x_1^1,x_1^2,x_1^3$). If P or T is given, then the whole system is determined. 





# Basics for Statistical Mechanics

The subject for stattistical mechanics is to find an interpetation for entropy. The folloing paragraph is important insight:

>  A realistic view of a macroscopicsystem is one in which the system makes enormously rapid random transitions among its quantum states. A macro- scopic measurement senses only an average of the properties of myriads of quantum states.

All "statistical mechanicians" agree with the preceding paragraph, but not all would agree on the *dominant* mechanism for inducing transitions.

Postulates: 

1. a macroscopic system samples every permissible quantum state with equal probability
2. The number of microstates among which the system undergoes transitions, and which thereby share uniform probability of occupation, increases to the maximum permitted by the imposed constraints.

By these hypothesis we get 
$$
S = k_B\ln \Omega
$$






















