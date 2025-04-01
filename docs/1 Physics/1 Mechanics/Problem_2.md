# Investigating the Dynamics of a Forced Damped Pendulum

#### 1. Theoretical Foundation

The motion of a forced damped pendulum is governed by a second-order nonlinear differential equation. For a pendulum of length $L$, mass $m$, under gravitational acceleration $g$, with damping coefficient $b$, and subjected to an external periodic force $F(t) = F_0 \cos(\omega t)$, the equation of motion is:

$$
mL\frac{d^2\theta}{dt^2} + b\frac{d\theta}{dt} + mg\sin\theta = F_0 \cos(\omega t)
$$

Dividing through by $mL$, we obtain the standard form:

$$
\frac{d^2\theta}{dt^2} + \frac{b}{mL}\frac{d\theta}{dt} + \frac{g}{L}\sin\theta = \frac{F_0}{mL}\cos(\omega t)
$$

Define the natural frequency $\omega_0 = \sqrt{\frac{g}{L}}$, the damping ratio $\gamma = \frac{b}{2mL}$, and the forcing amplitude $f = \frac{F_0}{mL}$. The equation becomes:

$$
\frac{d^2\theta}{dt^2} + 2\gamma\frac{d\theta}{dt} + \omega_0^2 \sin\theta = f \cos(\omega t)
$$

##### Small-Angle Approximation
For small angles $( \theta \ll 1 )$, $\sin\theta \approx \theta$, simplifying the equation to a linear forced damped oscillator:

$$
\frac{d^2\theta}{dt^2} + 2\gamma\frac{d\theta}{dt} + \omega_0^2 \theta = f \cos(\omega t)
$$

This is a linear second-order differential equation with a harmonic driving term. The general solution consists of a homogeneous solution (transient) and a particular solution (steady-state). The homogeneous equation is:

$$
\frac{d^2\theta}{dt^2} + 2\gamma\frac{d\theta}{dt} + \omega_0^2 \theta = 0
$$

The characteristic equation is $r^2 + 2\gamma r + \omega_0^2 = 0$, with roots:

$$
r = -\gamma \pm \sqrt{\gamma^2 - \omega_0^2}
$$


- If $\gamma$ < $\omega_0$ (underdamped), the solution is 
$$
 \theta_h(t) = e^{-\gamma t} (A \cos(\omega_d t) + B \sin(\omega_d t)) $, where $ \omega_d = \sqrt{\omega_0^2 - \gamma^2}. 
$$

- The particular solution for the forcing term $f\cos(\omega t)$ is:

$$
\theta_p(t) = C \cos(\omega t) + D \sin(\omega t)
$$

Using the method of undetermined coefficients, substitute into the equation and solve for $C$ and $D$:

$$
C = \frac{f (\omega_0^2 - \omega^2)}{(\omega_0^2 - \omega^2)^2 + (2\gamma\omega)^2}, \quad D = \frac{f (2\gamma\omega)}{(\omega_0^2 - \omega^2)^2 + (2\gamma\omega)^2}
$$

The amplitude of the steady-state solution is:

$$
A = \sqrt{C^2 + D^2} = \frac{f}{\sqrt{(\omega_0^2 - \omega^2)^2 + (2\gamma\omega)^2}}
$$

##### Resonance Conditions
Resonance occurs when the driving frequency $\omega$ approaches the natural frequency $\omega_0$. For minimal damping   $\gamma \to 0$, the amplitude $A$ peaks sharply at $\omega = \omega_0$, leading to a significant energy increase in the system. The maximum amplitude is approximately $\frac{f}{2\gamma\omega_0}$, illustrating how damping limits resonant growth.

#### 2. Analysis of Dynamics

The full nonlinear equation $(\sin\theta \neq \theta)$ introduces complexity beyond the small-angle regime. Key parameters influencing the dynamics include:

- **Damping Coefficient $(\gamma)$**: Higher damping reduces oscillation amplitude and suppresses chaotic behavior, stabilizing the system.

- **Driving Amplitude ($f$)**: Small $f$ leads to periodic motion; large $f$ can drive the system into chaos.

- **Driving Frequency ($\omega$)**: Near $\omega_0$, resonance enhances amplitude; far from $\omega_0$, quasiperiodic or chaotic motion may emerge.

The transition to chaos occurs when nonlinearity dominates, often observed through period-doubling bifurcations. For certain $f$ and $\omega$, the pendulum exhibits regular oscillations synchronized with the driving force. Increasing $f$ beyond a critical threshold destabilizes this motion, leading to unpredictable, chaotic trajectories sensitive to initial conditions.

#### 3. Practical Applications

The forced damped pendulum model applies to:

- **Energy Harvesting**: Piezoelectric devices convert mechanical oscillations into electrical energy, optimized near resonance.

- **Suspension Bridges**: Periodic wind forces can induce resonance or chaotic vibrations, necessitating damping design.

- **Oscillating Circuits**: Driven RLC circuits mirror the pendulum’s dynamics, used in signal processing.

#### 4. Implementation: Computational Model

We use Python with the Runge-Kutta 4th-order (RK4) method to solve the nonlinear equation numerically. Below is a sample implementation:
![Forced Damped Pendulum Motion](../images/image_1_P2.png)

![Phase Portrait](../images/image_2_P2.png)


#### Deliverables

1. **General Solutions**: The small-angle solution is derived above; nonlinear dynamics require numerical methods like RK4.

2. **Graphical Representations**: The code generates time series, phase portraits, and Poincaré sections for varying $\gamma$, $f$, and $\omega$. Resonance peaks at $\omega \approx \omega_0$; chaos emerges with large $f$ (e.g., $f = 1.5$).

3. **Limitations and Extensions**: The model assumes constant parameters and periodic forcing. Nonlinear damping $(b|\dot{\theta}|)$ or stochastic forcing could enhance realism.

4. **Complex Dynamics**: Phase portraits show closed loops for periodic motion and scattered points for chaos. Poincaré sections and bifurcation diagrams (varying $f$) reveal transitions to chaos.
