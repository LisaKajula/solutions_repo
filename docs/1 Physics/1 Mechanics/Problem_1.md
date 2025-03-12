
# Investigating the Range as a Function of the Angle of Projection

## 1. Theoretical Foundation

Projectile motion is a classic physics problem where an object moves under gravity alone after an initial launch. We’ll derive the equations from Newton’s laws, assuming constant gravitational acceleration $g$.

### Governing Equations
*Notes*: We start with a projectile launched from the origin $(x_0, y_0) = (0, 0)$ with initial speed $v_0$ at angle $\theta$. The velocity splits into horizontal and vertical components, and gravity only acts downward.

- Initial velocity components:
  - $v_{x0} = v_0 \cos\theta$ (horizontal, constant since no horizontal acceleration)
  - $v_{y0} = v_0 \sin\theta$ (vertical, affected by gravity)
- Acceleration:
  - $a_x = 0$ (no horizontal force)
  - $a_y = -g$ (gravity downward)

Using kinematic equations $x(t) = x_0 + v_{x0}t + \frac{1}{2}a_x t^2$ and $y(t) = y_0 + v_{y0}t + \frac{1}{2}a_y t^2$:
- Horizontal: $$x(t) = v_0 \cos\theta \cdot t$$
- Vertical: $$y(t) = v_0 \sin\theta \cdot t - \frac{1}{2} g t^2$$

*Notes*: These are the parametric equations of motion. The horizontal motion is linear (constant velocity), while the vertical motion is quadratic (parabolic due to gravity).

### Time of Flight
*Notes*: The time of flight $T$ is when the projectile returns to $y = 0$ (assuming flat ground). Solve $y(t) = 0$:
$$0 = v_0 \sin\theta \cdot t - \frac{1}{2} g t^2$$
Factor out $t$:
$$t (v_0 \sin\theta - \frac{1}{2} g t) = 0$$
Solutions:
- $t = 0$ (launch time)
- $v_0 \sin\theta - \frac{1}{2} g t = 0 \implies t = \frac{2 v_0 \sin\theta}{g}$

Thus, time of flight: $$T = \frac{2 v_0 \sin\theta}{g}$$

*Notes*: $T$ depends on $v_0$, $\theta$, and $g$. At $\theta = 0^\circ$ or $90^\circ$, $T$ adjusts accordingly (minimal or maximal vertical motion).

### Range
*Notes*: The range $R$ is the horizontal distance at $t = T$. Substitute $T$ into $x(t)$:
$$R = x(T) = v_0 \cos\theta \cdot \frac{2 v_0 \sin\theta}{g} = \frac{2 v_0^2 \sin\theta \cos\theta}{g}$$
Use the trigonometric identity $2 \sin\theta \cos\theta = \sin(2\theta)$:
$$R = \frac{v_0^2 \sin(2\theta)}{g}$$

*Notes*: This is the key equation—a family of solutions parameterized by $v_0$ (initial speed), $\theta$ (angle), and $g$ (gravity). It’s symmetric about $\theta = 45^\circ$ due to $\sin(2\theta)$.

## 2. Analysis of the Range

*Notes*: Let’s explore how $R$ changes with its parameters.

- **Angle ($\theta$)**: Since $\sin(2\theta)$ ranges from 0 to 1:
  - Maximum at $2\theta = 90^\circ \implies \theta = 45^\circ$, where $$R_{\text{max}} = \frac{v_0^2}{g}$$
  - Zero at $\theta = 0^\circ$ or $90^\circ$ (no horizontal travel).
- **Velocity ($v_0$)**: $R \propto v_0^2$, so doubling $v_0$ quadruples $R$.
- **Gravity ($g$)**: $R \propto \frac{1}{g}$, so lower gravity (e.g., Moon’s $g = 1.62 \, \text{m/s}^2$ vs. Earth’s $9.81 \, \text{m/s}^2$) increases $R$.

*Notes*: The $45^\circ$ optimum balances horizontal and vertical motion. Varying $v_0$ or $g$ scales the range, which we’ll visualize.

## 3. Practical Applications

*Notes*: This ideal model applies broadly but can be adapted:
- **Uneven Terrain**: If landing at height $h$, solve $y(t) = h$, adjusting $T$ and $R$.
- **Air Resistance**: Add a drag force like $$F_d = -k v^2$$, requiring numerical methods (e.g., Euler or Runge-Kutta).
- **Real-World Examples**:
  - Sports: A kicked soccer ball’s range depends on $\theta$ and $v_0$, modified by spin.
  - Engineering: Rocket trajectories optimize $\theta$ for distance or orbit.

*Notes*: These extensions show the model’s versatility beyond the ideal case.

## 4. Implementation

*Notes*: We’ll simulate $R$ vs. $\theta$ using Python, comparing different $v_0$ and $g$ values.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g_earth = 9.81  # m/s^2 (Earth gravity)
g_moon = 1.62   # m/s^2 (Moon gravity)
v0 = 20.0       # m/s (initial speed)

# Range function
def range_projectile(v0, theta_deg, g):
    theta = np.radians(theta_deg)  # Convert degrees to radians for sin/cos
    return (v0**2 * np.sin(2 * theta)) / g  # Range formula

# Angles from 0 to 90 degrees
theta_deg = np.linspace(0, 90, 91)  # 91 points for smooth curve

# Compute ranges for different conditions
R_earth = range_projectile(v0, theta_deg, g_earth)          # Earth, base v0
R_moon = range_projectile(v0, theta_deg, g_moon)            # Moon, base v0
R_v0_double = range_projectile(2 * v0, theta_deg, g_earth)  # Earth, doubled v0

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(theta_deg, R_earth, label=f'Earth (g = {g_earth} m/s², v0 = {v0} m/s)')
plt.plot(theta_deg, R_moon, label=f'Moon (g = {g_moon} m/s², v0 = {v0} m/s)')
plt.plot(theta_deg, R_v0_double, label=f'Earth (g = {g_earth} m/s², v0 = {2*v0} m/s)')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (meters)')
plt.title('Projectile Range vs. Angle of Projection')
plt.grid(True)
plt.legend()
plt.show()

# Find and print maximum range on Earth
max_idx = np.argmax(R_earth)
print(f"Max range on Earth: {R_earth[max_idx]:.2f} m at {theta_deg[max_idx]}°")
```

*Notes on Code*:
- **Function**: `range_projectile` implements $R = \frac{v_0^2 \sin(2\theta)}{g}$, converting $\theta$ to radians.
- **Data**: Computes $R$ for $\theta = 0^\circ$ to $90^\circ$ under three conditions:
  1. Earth gravity, base speed.
  2. Moon gravity, base speed (larger range due to lower $g$).
  3. Earth gravity, doubled speed (quadrupled range due to $v_0^2$).
- **Plot**: Visualizes the parabolic dependence on $\theta$, peaking at $45^\circ$.
- **Output**: Confirms the max range numerically.

## Discussion on Limitations

*Notes*: The model assumes:
- No air resistance (drag would reduce $R$, especially at high $v_0$).
- Flat terrain (height changes alter $T$ and $R$).
- Constant $g$ (true near Earth’s surface, less so for high altitudes).

*Improvements*:
- **Drag**: Add $$F_d = -k v^2$$ and solve numerically.
- **Terrain**: Adjust for $y(t) = h$, modifying $T$.
- **Wind**: Include a horizontal velocity term.

*Notes*: These extensions make the model more realistic, connecting it to practical physics problems.

---

### Rendering and Running in VS Code
- **File**: Save as `projectile_motion.md`.
- **Rendering**: With "Markdown+Math" installed, preview (`Ctrl+Shift+V`) should show $inline$ and $$block$$ equations nicely.
- **Code**: Extract the Python to `projectile.py` or run in a Jupyter notebook (install "Jupyter" extension, create `.ipynb`, paste code into a cell).
- **Requirements**: Install `numpy` and `matplotlib` (`pip install numpy matplotlib`).

### Output Notes
- The plot will show three curves, with peaks at $45^\circ$.
- Max range on Earth (at $v_0 = 20 \, \text{m/s}$, $g = 9.81 \, \text{m/s}^2$) is about 40.77 m, confirming $R_{\text{max}} = \frac{v_0^2}{g} = \frac{400}{9.81}$.

