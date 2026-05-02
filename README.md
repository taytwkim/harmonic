# Harmonic Coordinates

![demo](img/demo.png)

A simple 2D demonstration of [Harmonic Coordinates for Character Articulation](https://graphics.pixar.com/library/HarmonicCoordinatesB/paper.pdf).

Learn more about this project in [this blog article](https://taytwkim.vercel.app/blog/projects/002-harmonic/).

## ⭐ Harmonic Coordinates

In cage-based deformation, a "cage" is defined around a target shape. The deformation of the shape is driven by manipulating the control points (vertices) of the cage. As the cage is deformed, we want the enclosed shape to follow smoothly.

To achieve this, we assign a set of weights to each interior point `p` relative to the cage control points `(c₁, ..., cₙ)`, such that: `p​ = ∑​ wi​(p) * c​i` and `∑ ci = 1`. These weights determine how much influence each control point has on the interior point. If `p` is closer to `c₁` than to `c₂`, then ideally `w₁ > w₂`.

After computing the weights once, we can deform the cage and compute the new position `p'` as: `p' = ∑​ wi​(p) * c'​i`.

![cage-based-deformation](img/cage-based-deformation.png)

In this project, we use **harmonic coordinates** — a type of weight function computed by minimizing the **Dirichlet energy** subject to boundary conditions. This leads to solving the Laplace equation, ensuring that the weights vary smoothly and produce natural-looking deformations.

![harmonic-weights](img/harmonic-weights.png)

Harmonic weights are especially useful for complex or non-convex cages, offering smooth and stable results.

## 🚀 Getting Started

* Set up a `venv`
```bash
python3.10 -m venv .venv # use python 3.10
source .venv/bin/activate
```

* Install packages
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

* Launch notebook
```bash
jupyter notebook
```

## ⚠️ Known Errors

`igl.grad` sometimes returns a matrix of 0s, causing an error. [Downgrading numpy](https://github.com/libigl/libigl-python-bindings/issues/242) seems to solve the problem.

```bash
pip install "numpy==1.26.4"
```
