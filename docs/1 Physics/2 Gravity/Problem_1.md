# 🌌 Gravity – Problem 1  
## Orbital Period and Orbital Radius

---

### 🧠 **Motivation**

The relationship between the square of the orbital period and the cube of the orbital radius, known as **Kepler's Third Law**, is a cornerstone of celestial mechanics.

This simple yet profound law allows scientists to:
- Determine planetary motion,
- Understand satellite orbits,
- Analyze cosmic systems governed by gravity.

---

### 🎯 **Task Overview**

1. **Derive** the relationship between the square of the orbital period and the cube of the orbital radius for circular orbits.  
2. **Discuss** implications for astronomy:
   - Estimating planetary masses and distances.
3. **Analyze** real-world examples:
   - Moon-Earth orbit.
   - Planetary orbits in the Solar System.
4. **Implement** a computational simulation to:
   - Model circular orbits.
   - Verify Kepler’s Third Law.

---

### 📘 **Theory: Kepler's Third Law**

In Newtonian mechanics, for a body of mass \( m \) orbiting a larger mass \( M \) at radius \( r \), the centripetal force is provided by gravity:

$$
\frac{G M m}{r^2} = \frac{m v^2}{r}
$$

Where:
- \( G \) is the gravitational constant,
- \( v \) is orbital velocity.

Solving for \( v \):

$$
v = \sqrt{\frac{G M}{r}}
$$

The orbital period \( T \) is:

$$
T = \frac{2\pi r}{v}
$$

Substituting for \( v \):

$$
T = 2\pi r \sqrt{\frac{r}{G M}} = 2\pi \sqrt{\frac{r^3}{G M}}
$$

Squaring both sides:

$$
T^2 = \frac{4\pi^2}{G M} \cdot r^3
$$

✅ This is **Kepler’s Third Law** in Newtonian form.

---

### 🔬 **Implications for Astronomy**

- Allows calculation of:
  - Planetary masses \( M \) using known orbits.
  - Orbital radii from observed periods.
- Used by astronomers and aerospace engineers for:
  - Mission planning.
  - Satellite deployment.
  - Understanding exoplanets.

---

### 🌍 **Real-World Examples**

#### 🌕 Moon Orbiting Earth

- Period: ~27.3 days  
- Radius: ~384,400 km

Compare observed \( T^2 \) and \( r^3 \) to verify the law.

#### 🪐 Planets in the Solar System

Plot \( T^2 \) vs \( r^3 \) for:
- Mercury to Neptune
- Expect a linear relationship on log-log plot

---

### 💻 **Python Simulation Snippet**

```python
import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11  # m^3/kg/s^2
M = 1.989e30     # Mass of the Sun in kg

# Orbital radii in meters (e.g., Earth to Mars)
radii = np.array([5.79e10, 1.08e11, 1.50e11, 2.28e11])  # Mercury to Mars

# Calculate periods
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))

# Plotting
plt.figure(figsize=(8,5))
plt.plot(radii**3, periods**2, 'o-', label='T² vs R³')
plt.xlabel('Orbital Radius Cubed (m³)')
plt.ylabel('Orbital Period Squared (s²)')
plt.title("Verification of Kepler's Third Law")
plt.legend()
plt.grid(True)
plt.show()
