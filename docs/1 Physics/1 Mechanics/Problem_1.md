# Problem 1

# Analytical and Computational Investigation of Projectile Range as a Function of Launch Angle

## Abstract
This study examines the dependence of a projectile’s horizontal range on its angle of projection, grounded in the principles of classical mechanics. Through analytical derivation and computational simulation, we explore the governing equations, analyze parametric influences, and assess practical applications. The investigation culminates in a Python-based simulation tool that visualizes range variations, accompanied by a discussion of model limitations and potential extensions.

## 1. Theoretical Foundation

### 1.1 Derivation of Governing Equations
Projectile motion under gravitational influence is modeled as two-dimensional kinematics with constant acceleration. Consider a Cartesian coordinate system where the $x$-axis is horizontal and the $y$-axis is vertical, with gravity acting downward. The acceleration vector is:

- $$a_x = 0$$,
- $$a_y = -g$$,

where $g$ denotes gravitational acceleration (typically $9.81$$\text{m/s}^2$ on Earth).

A projectile is launched with initial velocity $v_0$ at angle $\theta$ relative to the horizontal, from an initial height $h$. The initial velocity components are:
- $v_{0x} = v_0 \cos\theta$,
- $v_{0y} = v_0 \sin\theta$.

#### Horizontal Motion
With no horizontal acceleration ($a_x = 0$), the velocity remains constant:

$$ v_x(t) = v_{0x} = v_0 \cos\theta. $$

Integrating with initial position $x(0) = 0:$

$$x(t) = v_0 \cos\theta \cdot t. $$

#### Vertical Motion
Vertical acceleration ($a_y = -g$) yields:

$$v_y(t) = v_{0y} + a_y t = v_0 \sin\theta - g t.$$

Integrating with initial position $y(0) = h$:

$$
y(t) = h + v_0 \sin\theta \cdot t - \frac{1}{2} g t^2.$$

These equations describe a parabolic trajectory for $h = 0$, modified by the initial height when $h \neq 0$.

### 1.2 Parametric Family of Solutions
The solutions form a family parameterized by $v_0$, $\theta$, $g$, and $h$. Variations in these parameters yield distinct trajectories:
- $\theta$ adjusts the directional distribution of velocity.
- $v_0$ scales the magnitude of displacement.
- $g$ influences the trajectory’s curvature.
- $h$ shifts the vertical origin, affecting flight time and range.

## 2. Range Analysis

### 2.1 Derivation of Horizontal Range
The horizontal range $R$ is the $x$-displacement when $y(t) = 0$. Set the vertical position equation to zero:

$$
0 = h + v_0 \sin\theta \cdot t - \frac{1}{2} g t^2.
$$

Rearrange into a quadratic form:

$$
\frac{1}{2} g t^2 - v_0 \sin\theta \cdot t - h = 0.
$$
Solve using the quadratic formula, where $a = \frac{1}{2} g$, $b = -v_0 \sin\theta$, $c = -h:$

$$
t = \frac{v_0 \sin\theta \pm \sqrt{(v_0 \sin\theta)^2 - 4 \cdot \frac{1}{2} g \cdot (-h)}}{g} = \frac{v_0 \sin\theta \pm \sqrt{v_0^2 \sin^2\theta + 2 g h}}{g}. 
$$

The positive root represents the time of flight $t_f$. For $h = 0$:

$$t_f = \frac{2 v_0 \sin\theta}{g}.$$

Thus:

$$R = v_0 \cos\theta \cdot t_f = \frac{v_0^2 \sin(2\theta)}{g},$$

where $\sin(2\theta) = 2 \sin\theta \cos\theta$. The range peaks at $\theta = 45^\circ$, when $h = 0$.

### 2.2 Parametric Sensitivity
- **Initial Velocity**: $R \propto v_0^2$, exhibiting quadratic scaling.
- **Gravitational Acceleration**: $R \propto 1/g$, inversely proportional.
- **Initial Height**: Non-zero $h$ extends $t_f$, increasing $R$ and shifting the optimal angle below 45°.

## 3. Practical Applications
This model is adaptable to:

- **Sports Science**: Optimizing trajectories in archery or javelin.

- **Engineering**: Designing ballistic systems or fluid jets.

- **Planetary Physics**: Adjusting $g$ for extraterrestrial environments.

Extensions to uneven terrain or resistive forces require modified boundary conditions or numerical methods.

## 4. Computational Implementation

### 4.1 Simulation Algorithm
A Python script computes and visualizes $R(\theta)$ for varying parameters. The range function accounts for arbitrary $h$:

```python
import numpy as np
import matplotlib.pyplot as plt

def compute_range(v0, theta_deg, g=9.81, h=0):
    """Compute horizontal range for given parameters."""
    theta = np.radians(theta_deg)
    discriminant = v0**2 * np.sin(theta)**2 + 2 * g * h
    if discriminant < 0:
        return 0
    t_flight = (v_0 * np.sin(theta) + np.sqrt(discriminant)) / g
    return v_0 * np.cos(theta) * t_flight

# Simulation parameters
v0_values = [10, 15, 20]  # Initial velocities (m/s)
h_values = [0, 10]        # Initial heights (m)
g = 9.81                  # Gravitational acceleration (m/s^2)
theta = np.linspace(0, 90, 91)  # Angles (degrees)

# Visualization
plt.figure(figsize=(10, 6))
for v0 in v0_values:
    for h in h_values:
        R = [compute_range(v0, t, g, h) for t in theta]
        plt.plot(theta, R, label=f'$v_0={v0}$ m/s, $h={h}$ m')
plt.xlabel('Projection Angle ($^\circ$)')
plt.ylabel('Range (m)')
plt.title('Projectile Range as a Function of Launch Angle')
plt.legend()
plt.grid(True)
plt.show()

# Analytical verification
theta_opt = 45
R_max = compute_range(20, theta_opt, g, 0)
print(f"Optimal angle (h=0): {theta_opt}°")
print(f"Maximum range (v0=20 m/s, h=0): {R_max:.2f} m")
```

### 4.2 Results
The script generates curves of $R$ versus $\theta$, illustrating:
- Peak range at 45° for $h = 0$.
- Shifted optima and extended ranges for $h > 0$.
- Quadratic scaling with $v_0$.

## 5. Discussion

### 5.1 Model Limitations
The idealized model neglects:

- Air resistance, which reduces range and alters trajectories.

- Environmental factors like wind or terrain slope.

- Rotational effects (e.g., Magnus force).

### 5.2 Proposed Extensions

- **Drag Inclusion**: Incorporate $-k v^2$ terms, solved via numerical integration (e.g., Runge-Kutta).

- **Complex Environments**: Model wind or variable $g$ for planetary applications.

- **Validation**: Compare with experimental data from physical systems.

## Conclusion
This investigation elucidates the interplay between launch angle and range, offering a robust framework for theoretical and applied physics. The computational tool enhances understanding, while proposed extensions address real-world complexities.

