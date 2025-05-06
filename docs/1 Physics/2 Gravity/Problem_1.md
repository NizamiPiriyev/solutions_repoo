# Problem 1


# Orbital Period and Orbital Radius: A Deep Dive into Kepler's Third Law

## Introduction

Kepler's Third Law, which relates the square of a celestial body's orbital period ($T^2$) to the cube of its orbital radius ($r^3$), is a fundamental principle in physics and astronomy. This law, first formulated by Johannes Kepler in the early 17th century, provides a mathematical framework for understanding how objects move under gravitational forces. It is essential for studying planetary systems, satellite orbits, and even distant exoplanets. This document derives the law for circular orbits, explores its astronomical implications, provides real-world examples, and includes a computational model to simulate and verify the relationship. The discussion is tailored for a physics student, balancing clarity with sufficient depth to ensure a robust understanding suitable for academic success.

## Derivation of Kepler's Third Law for Circular Orbits

To derive Kepler's Third Law, consider a small body (mass $m$) in a circular orbit around a much larger body (mass $M$), such as a planet orbiting the Sun or a satellite orbiting Earth. Two forces govern the motion:

1. **Gravitational Force**: According to Newton's law of universal gravitation, the force between the two bodies is:

$$
F_g = \frac{G M m}{r^2}
$$

where $G$ is the gravitational constant ($6.67430 \times 10^{-11}$, $\text{m}^3 \text{kg}^{-1} \text{s}^{-2}$), and $r$ is the distance between the centers of the two bodies (orbital radius).

2. **Centripetal Force**: For circular motion, the centripetal force required to keep the smaller body in orbit is:

$$
F_c = \frac{m v^2}{r}
$$

where $v$ is the orbital velocity.

Since the gravitational force provides the centripetal force, equate them:

$$
\frac{m v^2}{r} = \frac{G M m}{r^2}
$$

Cancel $m$ (assuming $m \neq 0$) and multiply both sides by $r$:

$$
v^2 = \frac{G M}{r}
$$

The orbital velocity can also be expressed in terms of the orbital period $T$, the time for one complete orbit. The circumference of the circular orbit is $2 \pi r$, so:

$$
v = \frac{2 \pi r}{T}
$$

Square this velocity:

$$
v^2 = \frac{4 \pi^2 r^2}{T^2}
$$

Substitute into the force balance equation:

$$
\frac{4 \pi^2 r^2}{T^2} = \frac{G M}{r}
$$

Multiply both sides by $T^2$ and $r$:

$$
4 \pi^2 r^3 = G M T^2
$$

Rearrange to isolate $T^2$:

$$
T^2 = \frac{4 \pi^2}{G M} r^3
$$

This is Kepler's Third Law for circular orbits, showing that the square of the orbital period is proportional to the cube of the orbital radius. The constant $\frac{4 \pi^2}{G M}$ depends on the mass of the central body.

## Implications for Astronomy

Kepler's Third Law is a powerful tool in astronomy with wide-ranging applications:

- **Determining Masses**: By measuring $T$ and $r$, the mass of the central body $M$ can be calculated:

$$
M = \frac{4 \pi^2 r^3}{G T^2}
$$

This is crucial for estimating the masses of planets, stars, and even black holes when observing orbiting objects like moons, satellites, or companion stars.

- **Calculating Orbital Radii**: If $M$ is known (e.g., the Sun’s mass), the orbital radius $r$ can be determined from the observed period $T$. This is used to map planetary orbits or design satellite trajectories.

- **Exoplanet Discovery**: For exoplanets, Kepler’s Third Law helps infer orbital distances and stellar masses by analyzing transit periods, aiding in the characterization of distant solar systems.

- **Satellite and Spacecraft Orbits**: Engineers use the law to design orbits for communication satellites, ensuring specific periods (e.g., geostationary orbits with $T = 24 \, \text{hours}$).

- **Galactic Dynamics**: The law extends to stars orbiting galactic centers, helping estimate the mass of galaxies or detect supermassive black holes.

## Real-World Examples

### 1. The Moon’s Orbit Around Earth

- **Orbital Radius**: $r \approx 384,400 \, \text{km} = 3.844 \times 10^8 \, \text{m}$
- **Orbital Period**: $T \approx 27.32 \, \text{days} = 2.36 \times 10^6 \, \text{s}$
- **Earth’s Mass Calculation**:

$$
M = \frac{4 \pi^2 (3.844 \times 10^8)^3}{(6.67430 \times 10^{-11}) (2.36 \times 10^6)^2}
$$

$$
M \approx 5.97 \times 10^{24} \, \text{kg}
$$

This matches Earth’s known mass, confirming the law’s accuracy.

### 2. Mars’ Orbit Around the Sun

- **Orbital Radius**: $r \approx 227.9 \times 10^6 \, \text{km} = 2.279 \times 10^{11} \, \text{m}$
- **Orbital Period**: $T \approx 687 \, \text{days} = 5.936 \times 10^7 \, \text{s}$
- **Sun’s Mass Calculation**:

$$
M = \frac{4 \pi^2 (2.279 \times 10^{11})^3}{(6.67430 \times 10^{-11}) (5.936 \times 10^7)^2}
$$

$$
M \approx 1.989 \times 10^{30} \, \text{kg}
$$

This aligns with the Sun’s known mass, validating the law for solar system scales.

### 3. Geostationary Satellites

- **Orbital Period**: $T = 24 \, \text{hours} = 86,400 \, \text{s}$
- **Earth’s Mass**: $M = 5.972 \times 10^{24} \, \text{kg}$
- **Orbital Radius**:

$$
r^3 = \frac{G M T^2}{4 \pi^2}
$$

$$
r^3 = \frac{(6.67430 \times 10^{-11}) (5.972 \times 10^{24}) (86,400)^2}{4 \pi^2}
$$

$$
r \approx 4.22 \times 10^7 \, \text{m} \approx 42,200 \, \text{km}
$$

This radius places the satellite at approximately 35,786 km above Earth’s surface, consistent with geostationary orbits.

## Computational Model

The following Python script simulates circular orbits and verifies Kepler’s Third Law by plotting $T^2$ versus $r^3$. It includes calculations for the Moon and Mars and visualizes their orbits.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M_earth = 5.972e24  # Earth's mass (kg)
M_sun = 1.989e30  # Sun's mass (kg)

def orbital_period(r, M):
    """Calculate orbital period given radius and central mass."""
    return np.sqrt((4 * np.pi**2 * r**3) / (G * M))

# Real-world examples
r_moon = 3.844e8  # Moon's orbital radius (m)
T_moon = orbital_period(r_moon, M_earth) / (3600 * 24)  # days
r_mars = 2.279e11  # Mars' orbital radius (m)
T_mars = orbital_period(r_mars, M_sun) / (3600 * 24)  # days

print(f"Moon: T = {T_moon:.2f} days, r = {r_moon/1e6:.2f} x 10^6 m")
print(f"Mars: T = {T_mars:.2f} days, r = {r_mars/1e9:.2f} x 10^9 m")

# T^2 vs r^3 plot
r = np.logspace(6, 12, 100)
T_earth = orbital_period(r, M_earth)
T_sun = orbital_period(r, M_sun)

plt.figure(figsize=(10, 7))
plt.loglog(r**3, T_earth**2, label="Earth-based orbits", linewidth=2)
plt.loglog(r**3, T_sun**2, label="Sun-based orbits", linewidth=2)
plt.scatter([r_moon**3, r_mars**3], [T_moon**2 * (3600 * 24)**2, T_mars**2 * (3600 * 24)**2], 
            color='red', s=100, label="Moon, Mars")
plt.xlabel("Orbital Radius Cubed (m³)", fontsize=12)
plt.ylabel("Orbital Period Squared (s²)", fontsize=12)
plt.title("Kepler's Third Law: T² vs r³", fontsize=14)
plt.legend(fontsize=10)
plt.grid(True, which="both", ls="--")
plt.savefig("kepler_third_law.png")
plt.close()

# Circular orbit simulation
def simulate_orbit(r, M, steps=100):
    """Simulate circular orbit coordinates."""
    T = orbital_period(r, M)
    theta = np.linspace(0, 2 * np.pi, steps)
    x = r * np.cos(theta)
    y = r * np.sin(theta)
    return x, y

x_moon, y_moon = simulate_orbit(r_moon, M_earth)
x_mars, y_mars = simulate_orbit(r_mars, M_sun)

plt.figure(figsize=(10, 10))
plt.plot(x_moon/1e6, y_moon/1e6, label="Moon's Orbit", linewidth=2)
plt.plot(x_mars/1e12, y_mars/1e12, label="Mars' Orbit (scaled)", linewidth=2)
plt.scatter([0], [0], color='red', s=200, label="Central Body")
plt.xlabel("X (10⁶ m for Moon, 10¹² m for Mars)", fontsize=12)
plt.ylabel("Y (10⁶ m for Moon, 10¹² m for Mars)", fontsize=12)
plt.title("Circular Orbits: Moon and Mars", fontsize=14)
plt.legend(fontsize=10)
plt.grid(True)
plt.axis("equal")
plt.savefig("circular_orbits.png")
plt.close()
```

![Sampling Distribution of the Sample Mean Population: Uniform](../images/image_G1_1.png)

![Sampling Distribution of the Sample Mean Population: Uniform](../images/image_G1_2.png)




### Output Explanation

- **T^2 vs r^3 Plot**: The logarithmic plot shows a linear relationship, confirming $T^2 \propto r^3$. Data points for the Moon and Mars align with the theoretical curves.
- **Orbit Simulation**: The circular paths illustrate the Moon’s and Mars’ orbits, with Mars’ orbit scaled down for visibility.

## Extension to Elliptical Orbits

While the derivation assumes circular orbits, Kepler’s Third Law applies to elliptical orbits by replacing the orbital radius $r$ with the semi-major axis $a$:

$$
T^2 = \frac{4 \pi^2}{G M} a^3
$$

- **Semi-Major Axis**: The average distance from the orbiting body to the central body, equal to half the longest diameter of the ellipse.
- **Applications**:
  - **Comets**: Halley’s Comet has $a \approx 17.8 \, \text{AU}$, $T \approx 76 \, \text{years}$.
  - **Exoplanets**: Kepler mission data use this law to estimate orbital periods and distances.
  - **Binary Stars**: The law helps calculate the masses of stars in binary systems.

The eccentricity of the ellipse affects the orbit’s shape but not the period, which depends solely on $a$.

## Practical Considerations and Limitations

- **Assumptions**: The derivation assumes a two-body system where one mass dominates, and external perturbations (e.g., other planets) are negligible.
- **Relativistic Effects**: For extreme cases (e.g., near black holes), general relativity modifies the relationship, but this is beyond Newtonian mechanics.
- **Measurement Precision**: Accurate $T$ and $a$ measurements are critical, as small errors are cubed or squared in calculations.

## Conclusion

Kepler’s Third Law is a cornerstone of celestial mechanics, linking orbital period and radius through gravitational principles. Its applications span from calculating Earth’s mass using the Moon’s orbit to designing satellite trajectories and studying exoplanets. The computational model verifies the law and visualizes orbits, providing a hands-on understanding. By extending to elliptical orbits, the law’s versatility is evident, making it a vital tool for physics and astronomy students.

