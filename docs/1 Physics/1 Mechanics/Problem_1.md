# Problem 1

# Investigating the Range as a Function of the Angle of Projection

## 1. Theoretical Foundation

### Deriving the Equations of Motion

Projectile motion is a classic example of two-dimensional motion under constant acceleration due to gravity. Let’s start with Newton’s second law and assume the only force acting is gravity (no air resistance for now). Define the coordinate system: \(x\) is horizontal (positive right), and \(y\) is vertical (positive up). The acceleration due to gravity is \(g\), acting downward.

The acceleration components are:
- \(a_x = 0\) (no horizontal forces),
- \(a_y = -g\).

Given initial velocity \(v_0\) at angle \(\theta\) from the horizontal, the initial velocity components are:
- \(v_{0x} = v_0 \cos\theta\),
- \(v_{0y} = v_0 \sin\theta\).

#### Horizontal Motion
Since \(a_x = 0\), the velocity is constant:
\[ v_x(t) = v_{0x} = v_0 \cos\theta. \]
Integrating with respect to time (initial position \(x_0 = 0\)):
\[ x(t) = v_0 \cos\theta \cdot t. \]

#### Vertical Motion
With \(a_y = -g\), integrate the acceleration:
\[ v_y(t) = v_{0y} - g t = v_0 \sin\theta - g t. \]
Integrate again (initial position \(y_0 = h\), the launch height):
\[ y(t) = h + v_0 \sin\theta \cdot t - \frac{1}{2} g t^2. \]

These are the parametric equations of motion. The trajectory is a parabola when \(h = 0\), but the launch height adds versatility.

### Family of Solutions
The parameters \(v_0\), \(\theta\), \(g\), and \(h\) define a family of solutions. For instance:
- Varying \(\theta\) changes the balance between horizontal and vertical components.
- Increasing \(v_0\) scales the trajectory’s size.
- Adjusting \(g\) (e.g., Earth vs. Moon) alters the curvature.
- Non-zero \(h\) shifts the starting point, affecting the range.

## 2. Analysis of the Range

### Range Derivation
The range \(R\) is the horizontal distance traveled when the projectile returns to \(y = 0\). Set \(y(t) = 0\):
\[ 0 = h + v_0 \sin\theta \cdot t - \frac{1}{2} g t^2. \]
Multiply through by 2 and rearrange:
\[ g t^2 - 2 v_0 \sin\theta \cdot t - 2h = 0. \]
This is a quadratic equation in \(t\):
\[ t = \frac{2 v_0 \sin\theta \pm \sqrt{(2 v_0 \sin\theta)^2 + 8 g h}}{2 g} = \frac{v_0 \sin\theta \pm \sqrt{v_0^2 \sin^2\theta + 2 g h}}{g}. \]
The positive root gives the time of flight. For \(h = 0\):
\[ t_f = \frac{2 v_0 \sin\theta}{g}. \]
Substitute into the horizontal position:
\[ R = v_0 \cos\theta \cdot t_f = v_0 \cos\theta \cdot \frac{2 v_0 \sin\theta}{g} = \frac{v_0^2 \cdot 2 \sin\theta \cos\theta}{g} = \frac{v_0^2 \sin(2\theta)}{g}. \]
This confirms the range depends on \(\sin(2\theta)\), peaking at \(\theta = 45^\circ\) when \(h = 0\).

### Parameter Influence
- **Initial Velocity (\(v_0\))**: \(R \propto v_0^2\), a quadratic increase.
- **Gravity (\(g\))**: \(R \propto 1/g\), so weaker gravity extends the range.
- **Launch Height (\(h\))**: For \(h > 0\), the time of flight increases, extending \(R\). The optimal angle shifts below 45°.

## 3. Practical Applications

This model applies to:
- **Sports**: Optimizing a basketball shot or golf drive.
- **Engineering**: Designing artillery or water fountains.
- **Astrophysics**: Trajectories on different planets (adjust \(g\)).

For uneven terrain, adjust the landing height in the equation. Air resistance requires numerical solutions (e.g., adding a drag term proportional to velocity squared), which we’ll simulate.

## 4. Implementation

### Python Script
Here’s a Python script using NumPy and Matplotlib to simulate and visualize the range.

```python
import numpy as np
import matplotlib.pyplot as plt

def range_projectile(v0, theta_deg, g=9.81, h=0):
    """Calculate range given initial velocity, angle (degrees), gravity, and height."""
    theta = np.radians(theta_deg)
    discriminant = v0**2 * np.sin(theta)**2 + 2 * g * h
    if discriminant < 0:
        return 0  # No real solution (doesn’t reach y=0)
    t_flight = (v0 * np.sin(theta) + np.sqrt(discriminant)) / g
    return v0 * np.cos(theta) * t_flight

# Parameters
v0_values = [10, 15, 20]  # m/s
g = 9.81  # m/s^2
h_values = [0, 10]  # m
theta = np.linspace(0, 90, 91)  # 0 to 90 degrees

# Plotting
plt.figure(figsize=(10, 6))
for v0 in v0_values:
    for h in h_values:
        R = [range_projectile(v0, t, g, h) for t in theta]
        plt.plot(theta, R, label=f'v0={v0} m/s, h={h} m')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (m)')
plt.title('Range vs. Angle of Projection')
plt.legend()
plt.grid(True)
plt.show()

# Optimal angle for h=0
theta_opt = 45
print(f"Optimal angle for h=0: {theta_opt}°")
R_max = range_projectile(20, theta_opt, g, 0)
print(f"Max range for v0=20 m/s, h=0: {R_max:.2f} m")
```

### Output Description
- **Graph**: Plots range vs. angle for different \(v_0\) and \(h\). Peaks shift with height.
- **Family of Solutions**: Curves vary with parameters, showing the model’s flexibility.

## Discussion

### Limitations
- **Idealized Model**: Ignores air resistance, wind, and spin.
- **Flat Earth**: Assumes constant \(g\) and no curvature.

### Enhancements
- **Drag**: Add \(-k v^2\) terms to the equations and solve numerically (e.g., using Euler or Runge-Kutta methods).
- **Wind**: Include horizontal acceleration terms.
- **Terrain**: Model \(y_{\text{land}}(x)\) and solve for intersection.

This exploration reveals projectile motion’s elegance and adaptability, bridging theory and application across physics and beyond.
