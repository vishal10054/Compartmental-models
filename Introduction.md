# Compartmental-Models
Compartmental models are a common framework used in epidemiology to model the spread of infectious diseases. These models divide the population into different compartments based on their disease status, such as Susceptible (S), Exposed (E), Infected (I), and Recovered (R).

Here we will be looking at the **SIERS** model and the **SIRS** model with **Vaccination**.

## SIERS Model
This model is an extension of the classic SEIR model that incorporates **waning immunity**, allowing individuals in the **Recovered (R)** compartment to eventually lose their immunity and return to the **Susceptible (S)** compartment. This makes the SEIRS model more realistic for diseases where immunity is not permanent such as COVID-19, influenza.

### <ins>Assumptions</ins>
**Waning Immunity**: Recovered individuals lose immunity at a rate δ and become susceptible again.

**Homogeneous Population**: The population is well-mixed, meaning everyone has an equal chance of interacting with everyone else.

**Constant Population Size**: Births and deaths are balanced, keeping the total population N=S+E+I+R constant.

### <ins>Equations Governing SIERS model</ins>
$$
\frac{dS}{dt} = μN - β\frac{SI}{N} + δR - μS
$$
$$
\frac{dE}{dt} = β\frac{SI}{N} - (α+μ)E
$$
$$
\frac{dI}{dt} = αE - (γ+μ)I
$$
$$
\frac{dR}{dt} = γI - (δ+μ)R
$$

### <ins>Parameters</ins>
**β**: Transmission rate (rate at which susceptible individuals become infected).

**α**: Rate at which exposed individuals become infectious (inverse of the incubation period).

**γ**: Recovery rate (inverse of the infectious period).

**δ**: Rate of waning immunity (inverse of the duration of immunity).

**μ**: Birth and death rate (assumes equal birth and death rates to keep the population constant).

## SIRS Model with Vaccination
When vaccination is introduced, a fraction of the susceptible population is moved directly to the recovered compartment, assuming the vaccine provides immunity.  
### <ins>Assumptions</ins>  
**Homogeneous Population**: The population is well-mixed, meaning every individual has an equal chance of interacting with any other individual.  

**Constant Population Size**: The total population N=S+I+R is constant (no births, deaths, or migration).  

**Vaccination**: A fraction p of susceptible individuals is vaccinated per unit time, moving them directly to the recovered compartment.  


### <ins>Equations governing SIRS with vaccination Model</ins>
$$
\frac{dS}{dt} = - βSI + δR - pS
$$
$$
\frac{dI}{dt} = βSI -γI
$$
$$
\frac{dR}{dt} = γI - δR + pS
$$
### <ins>Parameters</ins>
**β**: Transmission rate (rate at which susceptible individuals become infected).

**p**: Vaccination rate

**γ**: Recovery rate (inverse of the infectious period).

**δ**: Rate at which recorded indiiduals lose immunity and become susceptible again.





















