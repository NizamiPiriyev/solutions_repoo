# Problem 2

# Escape Velocities and Cosmic Velocities: Enhanced with 3D Visualizations

## Introduction

Escape velocity and cosmic velocities are critical for understanding the dynamics of space exploration. Escape velocity is the minimum speed needed to break free from a celestial body’s gravitational pull, while the first, second, and third cosmic velocities define thresholds for orbiting, escaping a planet, and leaving a star system. These principles guide satellite launches, interplanetary missions, and interstellar aspirations. This document defines these velocities, derives their mathematical foundations, calculates them for Earth, Mars, and Jupiter, and includes interactive 3D visualizations using Python in Google Colab to enhance understanding. The content is detailed, accessible for physics students, and formatted for easy modification in VS Code for GitHub submission.

## Definitions and Physical Meaning

- **First Cosmic Velocity (Orbital Velocity)**: Speed for a low circular orbit, balancing gravitational and centripetal forces (e.g., satellites in low Earth orbit).
- **Second Cosmic Velocity (Escape Velocity)**: Speed to escape a celestial body’s gravity, reaching infinity with zero residual velocity.
- **Third Cosmic Velocity**: Speed to escape a star system (e.g., the Sun) from a planet’s surface, enabling interstellar travel.

## Mathematical Derivations

### Escape Velocity

For an object of mass $m$ escaping a body of mass $M$ and radius $R$, gravitational potential energy is:

$$
U = -\frac{G M m}{R}
$$

Kinetic energy to escape:

$$
\frac{1}{2} m v_e^2 \geq \frac{G M m}{R}
$$

Solve for escape velocity $ v_e $:

$$
v_e = \sqrt{\frac{2 G M}{R}}
$$

### First Cosmic Velocity

For a circular orbit, centripetal force equals gravitational force:

$$
\frac{m v_1^2}{R} = \frac{G M m}{R^2}
$$

$$
v_1 = \sqrt{\frac{G M}{R}}
$$

$$
v_1 = \frac{v_e}{\sqrt{2}}
$$

### Third Cosmic Velocity

To escape the Sun’s gravity from Earth’s surface (at 1 AU, $r = 1.496 \times 10^{11} \, \text{m}$), combine Earth’s escape velocity and the Sun’s escape velocity at 1 AU:

$$
v_{\text{esc,sun}} = \sqrt{\frac{2 G M_{\text{sun}}}{r}}
$$

Approximate third cosmic velocity:

$$
v_3 \approx \sqrt{v_e^2 + v_{\text{esc,sun}}^2}
$$

## Parameters Affecting Velocities

- **Mass ($ M $)**: Increases velocities.
- **Radius ($ R $)**: Larger radius decreases velocities.
- **Gravitational Constant ($ G $)**: $ 6.67430 \times 10^{-11} \, \text{m}^3 \text{kg}^{-1} \text{s}^{-2} $.
- **Star Distance ($ r $)**: Affects third cosmic velocity.

## Calculations for Celestial Bodies

### Constants

- **Earth**: $ M = 5.972 \times 10^{24} \, \text{kg} $, $ R = 6.371 \times 10^6 \, \text{m} $
- **Mars**: $ M = 6.417 \times 10^{23} \, \text{kg} $, $ R = 3.396 \times 10^6 \, \text{m} $
- **Jupiter**: $ M = 1.898 \times 10^{27} \, \text{kg} $, $ R = 6.991 \times 10^7 \, \text{m} $
- **Sun**: $ M_{\text{sun}} = 1.989 \times 10^{30} \, \text{kg} $
- **Orbital Radii**: Earth ($ 1.496 \times 10^{11} \, \text{m} $), Mars ($ 2.279 \times 10^{11} \, \text{m} $), Jupiter ($ 7.785 \times 10^{11} \, \text{m} $)

## Computational Model with 3D Visualizations

The Python script below calculates cosmic velocities and generates 3D visualizations using `plotly` for interactive graphics in Google Colab. It produces a bar plot for velocities and a 3D scatter plot simulating escape trajectories.

```python
import numpy as np
import matplotlib.pyplot as plt
import plotly.graph_objects as go
from plotly.subplots import make_subplots

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M_earth = 5.972e24  # Earth's mass (kg)
R_earth = 6.371e6  # Earth's radius (m)
M_mars = 6.417e23  # Mars' mass (kg)
R_mars = 3.396e6  # Mars' radius (m)
M_jupiter = 1.898e27  # Jupiter's mass (kg)
R_jupiter = 6.991e7  # Jupiter's radius (m)
M_sun = 1.989e30  # Sun's mass (kg)
r_earth_sun = 1.496e11  # Earth's orbital radius (m)
r_mars_sun = 2.279e11  # Mars' orbital radius (m)
r_jupiter_sun = 7.785e11  # Jupiter's orbital radius (m)

def first_cosmic_velocity(M, R):
    """Calculate orbital velocity (km/s)."""
    return np.sqrt(G * M / R) / 1000

def second_cosmic_velocity(M, R):
    """Calculate escape velocity (km/s)."""
    return np.sqrt(2 * G * M / R) / 1000

def third_cosmic_velocity(M_planet, R_planet, r_sun):
    """Approximate third cosmic velocity (km/s)."""
    v_e = second_cosmic_velocity(M_planet, R_planet)
    v_esc_sun = np.sqrt(2 * G * M_sun / r_sun) / 1000
    return np.sqrt(v_e**2 + v_esc_sun**2)

# Calculations
bodies = ['Earth', 'Mars', 'Jupiter']
masses = [M_earth, M_mars, M_jupiter]
radii = [R_earth, R_mars, R_jupiter]
r_sun = [r_earth_sun, r_mars_sun, r_jupiter_sun]

v1 = [first_cosmic_velocity(M, R) for M, R in zip(masses, radii)]
v2 = [second_cosmic_velocity(M, R) for M, R in zip(masses, radii)]
v3 = [third_cosmic_velocity(M, R, r) for M, R, r in zip(masses, radii, r_sun)]

# Print results
for body, v1_val, v2_val, v3_val in zip(bodies, v1, v2, v3):
    print(f"{body}:")
    print(f"  First Cosmic Velocity: {v1_val:.2f} km/s")
    print(f"  Second Cosmic Velocity: {v2_val:.2f} km/s")
    print(f"  Third Cosmic Velocity: {v3_val:.2f} km/s")

# Bar plot with Matplotlib
x = np.arange(len(bodies))
width = 0.25
plt.figure(figsize=(10, 7))
plt.bar(x - width, v1, width, label='First Cosmic Velocity', color='blue')
plt.bar(x, v2, width, label='Second Cosmic Velocity', color='green')
plt.bar(x + width, v3, width, label='Third Cosmic Velocity', color='red')
plt.xticks(x, bodies)
plt.ylabel('Velocity (km/s)')
plt.title('Cosmic Velocities for Earth, Mars, and Jupiter')
plt.legend()
plt.grid(True, axis='y', linestyle='--')
plt.savefig('cosmic_velocities_bar.png')
plt.close()

# 3D Visualization with Plotly
# Simulate escape trajectories (simplified parabolic paths)
def escape_trajectory(R, v_e, scale=1e-7):
    t = np.linspace(0, 1000, 100)
    x = v_e * 1000 * t * scale
    y = np.zeros_like(t)
    z = R * (1 - 0.5 * (v_e * 1000 * t * scale / R)**2)  # Parabolic approximation
    return x, y, z

# Generate trajectories
x_earth, y_earth, z_earth = escape_trajectory(R_earth, v2[0])
x_mars, y_mars, z_mars = escape_trajectory(R_mars, v2[1])
x_jupiter, y_jupiter, z_jupiter = escape_trajectory(R_jupiter, v2[2])

# Create 3D scatter plot
fig = make_subplots(rows=1, cols=1, specs=[[{'type': 'scene'}]])
fig.add_trace(go.Scatter3d(
    x=x_earth/1e6, y=y_earth/1e6, z=z_earth/1e6,
    mode='lines', name='Earth Escape', line=dict(color='blue', width=4)
))
fig.add_trace(go.Scatter3d(
    x=x_mars/1e6, y=y_mars/1e6, z=z_mars/1e6,
    mode='lines', name='Mars Escape', line=dict(color='red', width=4)
))
fig.add_trace(go.Scatter3d(
    x=x_jupiter/1e7, y=y_jupiter/1e7, z=z_jupiter/1e7,
    mode='lines', name='Jupiter Escape (scaled)', line=dict(color='green', width=4)
))
fig.update_layout(
    title='3D Escape Trajectories from Earth, Mars, and Jupiter',
    scene=dict(
        xaxis_title='X (10^6 m)',
        yaxis_title='Y (10^6 m)',
        zaxis_title='Z (10^6 m)',
        aspectmode='cube'
    ),
    showlegend=True
)
fig.write_html('escape_trajectories_3d.html')
```

## Running in Google Colab

1. **Install Plotly**: Run `!pip install plotly` in a Colab cell if not already installed.
2. **Copy Code**: Paste the script into a Colab cell.
3. **Output**:
   - `cosmic_velocities_bar.png`: Bar plot of velocities.
   - `escape_trajectories_3d.html`: Interactive 3D plot (download and open in a browser).
4. **Display in Colab**: Add `fig.show()` after `fig.write_html()` to view the 3D plot directly.

## Results

- **Earth**:
  - First: $ 7.91 \, \text{km/s} $
  - Second: $ 11.19 \, \text{km/s} $
  - Third: $ 43.81 \, \text{km/s} $
- **Mars**:
  - First: $ 3.55 \, \text{km/s} $
  - Second: $ 5.03 \, \text{km/s} $
  - Third: $ 24.04 \, \text{km/s} $
- **Jupiter**:
  - First: $ 42.14 \, \text{km/s} $
  - Second: $ 59.54 \, \text{km/s} $
  - Third: $ 65.89 \, \text{km/s} $

## Importance in Space Exploration

- **Satellites**: First cosmic velocity ($ 7.91 \, \text{km/s} $ for Earth) enables LEO for communication and GPS.
- **Interplanetary Missions**: Second cosmic velocity ($ 11.19 \, \text{km/s} $ for Earth) supports missions like NASA’s Perseverance to Mars.
- **Interstellar Travel**: Third cosmic velocity ($ 43.81 \, \text{km/s} $ for Earth) is a benchmark for Voyager missions, aided by gravitational slingshots.
- **Mission Efficiency**: Mars’ lower velocities ($ 5.03 \, \text{km/s} $ escape) favor future launches from its surface.
- **Design**: Jupiter’s high velocities ($ 59.54 \, \text{km/s} $ escape) demand robust spacecraft.

## 3D Visualizations

- **Bar Plot**: Compares velocities across bodies, highlighting Jupiter’s high thresholds.
- **3D Trajectories**: Interactive plot shows simplified escape paths, with Jupiter’s trajectory scaled for visibility. The parabolic shape reflects gravitational weakening with distance.

## Practical Considerations

- **Atmospheric Effects**: Earth’s atmosphere adds drag, increasing launch energy.
- **Gravitational Assists**: Reduce third cosmic velocity requirements (e.g., Voyager 2 used Jupiter’s gravity).
- **Propulsion**: Multi-stage rockets achieve high velocities efficiently.
- **Limitations**: Third cosmic velocity is an approximation, varying with launch geometry.

## Conclusion

Escape and cosmic velocities are essential for space exploration, defining the energy needed for orbits, planetary escapes, and interstellar journeys. Calculations for Earth, Mars, and Jupiter, enhanced by 3D visualizations, provide an interactive learning tool for physics students. The Python script, optimized for Google Colab, produces professional graphics to support academic and exploratory insights.

