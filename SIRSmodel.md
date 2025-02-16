import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

# Define the SIRS model with vaccination
def sirs_model_with_vaccination(t, y, beta, gamma, delta, p, N):
    S, I, R = y
    dSdt = -beta * S * I / N + delta * R - p * S
    dIdt = beta * S * I / N - gamma * I
    dRdt = gamma * I - delta * R + p * S
    return [dSdt, dIdt, dRdt]

# Parameters
beta = 0.5  # Transmission rate
gamma = 0.1  # Recovery rate
delta = 0.01  # Waning immunity rate
p = 0.05     # Vaccination rate
N = 1000     # Total population

# Initial conditions (S0, I0, R0)
S0 = 990     # Initial susceptible population
I0 = 10      # Initial infectious population
R0 = 0       # Initial recovered population
y0 = [S0, I0, R0]

# Time span (0 to 365 days)
t_span = (0, 365)
t_eval = np.linspace(0, 365, 1000)  # Time points for evaluation

# Solve the system of ODEs
sol = solve_ivp(sirs_model_with_vaccination, t_span, y0, args=(beta, gamma, delta, p, N), 
                t_eval=t_eval, method='RK45')

# Extract results
S = sol.y[0]
I = sol.y[1]
R = sol.y[2]
time = sol.t

# Plot individual graphs for S, I, and R
plt.figure(figsize=(15, 5))

# Plot Susceptible (S)
plt.subplot(1, 3, 1)
plt.plot(time, S, label='Susceptible (S)', color='blue')
plt.xlabel('Time (days)')
plt.ylabel('Number of Individuals')
plt.title('Susceptible Population Over Time')
plt.legend()
plt.grid()

# Plot Infectious (I)
plt.subplot(1, 3, 2)
plt.plot(time, I, label='Infectious (I)', color='red')
plt.xlabel('Time (days)')
plt.ylabel('Number of Individuals')
plt.title('Infectious Population Over Time')
plt.legend()
plt.grid()

# Plot Recovered (R)
plt.subplot(1, 3, 3)
plt.plot(time, R, label='Recovered (R)', color='green')
plt.xlabel('Time (days)')
plt.ylabel('Number of Individuals')
plt.title('Recovered Population Over Time')
plt.legend()
plt.grid()

plt.tight_layout()
plt.show()

# Plot all compartments on the same graph
plt.figure(figsize=(10, 6))
plt.plot(time, S, label='Susceptible (S)', color='blue')
plt.plot(time, I, label='Infectious (I)', color='red')
plt.plot(time, R, label='Recovered (R)', color='green')
plt.xlabel('Time (days)')
plt.ylabel('Number of Individuals')
plt.title('SIRS Model with Vaccination')
plt.legend()
plt.grid()
plt.show()
