# Lorenz Attractor Visualizer

English | [日本語](README.ja.md)

A single-file, dependency-free visualizer for the Lorenz attractor. It integrates the Lorenz equations in real time in your browser and draws the trajectory in 3D. You can rotate it, change the parameters, and watch two almost identical starting points drift apart (the butterfly effect).

> The interface and the built-in explanation are in Japanese.

## What it shows

The Lorenz system ([Lorenz, 1963](#reference)) is three coupled differential equations, a drastically simplified model of convection in a fluid layer heated from below:

```
dx/dt = σ(y − x)
dy/dt = x(ρ − z) − y
dz/dt = xy − βz
```

With the classic values σ = 10, ρ = 28, β = 8/3, the system is chaotic. There is no randomness in the equations, yet a trajectory never repeats itself, and two trajectories that start very close together separate exponentially fast.

## Features

- Real-time integration with a 4th-order Runge–Kutta method (step size 0.005)
- 3D view with perspective: drag to rotate, mouse wheel or pinch to zoom, optional auto-rotation
- Three presets: a single long trajectory, two nearly identical points, and a swarm of points
- Live sliders for σ, ρ, β, simulation speed, trail length, and the number of orbits
- A log-scale plot of the distance between two orbits (shown when two or more orbits are running)
- Markers for the fixed points C₊ and C₋ (can be switched off)
- A short built-in explanation for beginners (in Japanese)
- Respects `prefers-reduced-motion`: auto-rotation starts off and the default speed is lower

## Presets

| Preset (label in the UI) | What it does |
| --- | --- |
| 一本の軌跡 (One trajectory) | Draws one long trail from a single starting point. |
| ほぼ同じ2点 (Two nearly identical points) | Runs two points whose starting values differ by 1e-5. They overlap at first, then split apart. The distance plot shows the exponential growth of the gap. |
| 点の群れ (A swarm) | Places 160 points inside a tiny ball and lets them stretch across the whole attractor. |

## Controls

| Control (label in the UI) | What it does |
| --- | --- |
| σ (プラントル数), ρ (加熱の強さ), β (形状係数) | The three parameters of the equations. Standard values: 10, 28, 8/3. |
| 標準値に戻す | Resets σ, ρ, β to the standard values. |
| 進む速さ | Integration steps per animation frame (1–20). |
| 軌跡の長さ | Number of points kept in each trail (20–12000). |
| 軌道の数 | Number of simultaneous orbits (1–300). The total number of drawn points is capped at 45,000. |
| 自動で回す | Toggles auto-rotation. |
| 不動点を表示 | Toggles the markers for the fixed points. |
| 一時停止 / 再開 | Pauses or resumes the simulation. |
| やり直し | Restarts from a fresh starting point. |

Try lowering ρ to about 10: the orbit no longer wanders between the two lobes and settles onto one of the fixed points.

## Usage

Open `lorenz.html` in a modern browser. There is no build step and nothing to install.

Fonts are loaded from Google Fonts. Offline, the page falls back to system fonts and works the same.

To host it, upload the single file to any static web host. For GitHub Pages, rename it to `index.html` and enable Pages for the repository.

If you share the page somewhere that shows link cards, add an `og:image` tag to the `<head>`. A commented-out example is already in the file.

## Notes

- At the standard values, a small difference between two orbits grows by a factor of about 2.5 per unit of simulation time. This is an estimate from numerical computation.
- The page uses Canvas 2D, Pointer Events, and `ResizeObserver`. Drawing many points can be heavy on low-end devices; reduce the number of orbits or the trail length if it stutters.

## Reference

E. N. Lorenz, "Deterministic Nonperiodic Flow", *Journal of the Atmospheric Sciences*, 20(2), 130–141 (1963).
