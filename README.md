# 🌀 Morris–Thorne Wormhole Embedding Dataset

This dataset provides a **numerically generated embedding diagram** of a Morris–Thorne–style traversable wormhole, represented as a 3D surface (`X`, `Y`, `Z`) and associated **energy density** field `ρ`.

---

## 📘 Description

The dataset contains sampled values from the **spatial embedding surface** of a spherically symmetric, static wormhole with shape function:

\[
b(r) = \frac{b_0^2}{r}
\]

and throat radius \( b_0 = 1.0 \).  
The embedding surface \( z(r) \) satisfies:

\[
\frac{dz}{dr} = \pm \sqrt{\frac{b(r)}{r - b(r)}}
\]

and is revolved around the z-axis to produce the full 3D geometry.  
Energy density is derived from the Einstein field equations:

\[
\rho(r) = \frac{b'(r)}{8\pi r^2}
\]

which is negative near the throat, indicating exotic matter.

---

## 📂 File Contents

| File | Description |
|------|--------------|
| `wormhole_embedding_b0_1.npz` | Compressed NumPy archive containing arrays `X`, `Y`, `Z`, `rho`, `r`, `z`, and `phi` |
| `wormhole_embedding_b0_1.xlsx` | Excel version (flattened into columns X, Y, Z, ρ) |

### Array Shapes

| Array | Shape | Meaning |
|--------|--------|----------|
| `X`, `Y`, `Z` | (200, 1600) | 3D coordinates of embedding surface |
| `rho` | (200, 1600) | Energy density mapped to the surface |
| `r`, `z` | (1600,) | Radial and embedding coordinates |
| `phi` | (200,) | Angular grid used for rotation |

---

## 🧩 Example Usage (Python)

```python
import numpy as np
import plotly.graph_objects as go

# Load dataset
data = np.load("wormhole_embedding_b0_1.npz")

# Extract arrays
X, Y, Z, rho = data["X"], data["Y"], data["Z"], data["rho"]

# Plot interactive wormhole embedding
fig = go.Figure(data=[go.Surface(x=X, y=Y, z=Z, surfacecolor=rho, colorscale="Viridis")])
fig.update_layout(
    title="Morris–Thorne Wormhole Embedding (b(r)=b₀²/r)",
    scene=dict(xaxis_title='X', yaxis_title='Y', zaxis_title='Z', aspectmode="data"),
    width=900, height=750
)
fig.show()
