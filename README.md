# QUANTA — Quantum State Clock

> The time is unknown. Until you decide to know it.

QUANTA is a single-page, dependency-free web experience that reimagines the clock through the lens of quantum mechanics. Instead of ticking numbers, it displays a drifting cloud of probability. Time stays undetermined until the system is **observed**, at which point the wavefunction collapses into a precise, glowing readout of hours, minutes, and seconds.

It's part interactive art piece, part physics metaphor, part clock.

🔗 **[Live demo](https://nazat02.github.io/QUANTA/)** · Landing page: `index.html` · Application: `simulation.html`

---

## Concept

QUANTA is built around three ideas borrowed from quantum theory:

| Principle | What it means in QUANTA |
|---|---|
| **Superposition** | Between observations, every possible time exists at once. Thousands of particles drift across the disc in a probabilistic fog — each point a candidate moment. |
| **Observation** | Looking is not passive. Pressing **Observe** (or simply returning to the tab) acts as a measurement, forcing the system to commit to a single value. |
| **Eigenstate** | Collapse is irreversible — for a moment. Three luminous spikes emerge (hours, minutes, seconds), each a definite "eigenvalue" of the time operator, before decoherence dissolves them back into the fog. |

Time is never displayed passively; it has to be observed to resolve.

---

## Features

- **Three rendering modes**, all visualizing the same underlying clock data:
  - **Particle** — thousands of independent probability points drifting in a bounded cloud, contracting to three labelled spikes on observation.
  - **Gaussian** — a smooth, continuous probability-density surface (bell curves per time dimension) that resolves into sharp peaks.
  - **3D** — a spherical s-orbital particle shell around a glowing nucleus, with clock spikes projected outward in 3D perspective. Draggable to rotate.
- **Auto-collapse on watch** — switching back to the browser tab, refocusing the window, or opening the page acts as an observation, mirroring the act of glancing at a wristwatch. Manual collapse via button, click, or spacebar also works.
- **Four color themes** — Blue, Red, Green, Yellow — switchable instantly via the theme picker.
- **Zoom & pan** — mouse wheel / pinch-to-zoom, click-and-drag panning, double-click or `0` to reset the view.
- **Keyboard shortcuts**:
  - `Space` — observe / collapse the wavefunction
  - `+` / `-` — zoom in / out
  - `0` — reset view
- **Touch support** — pinch-zoom and drag gestures on mobile/tablet.
- **Cinematic chrome** — ambient glow, scanlines, vignette, film grain, and corner markers for an instrument-panel aesthetic.
- **Animated landing page** (`index.html`) that explains the concept, walks through "how it works," and previews all three modes before linking to the live simulation.

---

## Tech stack

QUANTA is intentionally minimal:

- **Pure HTML, CSS, and vanilla JavaScript** — no frameworks, no build tools, no bundlers.
- **Canvas 2D** rendering for the particle/Gaussian clouds, driven by `requestAnimationFrame`.
- **No network requests after initial load** — once the page is open, it runs entirely offline.
- **Google Fonts** (`Cormorant Garamond`, `Space Mono`, `Inter`) loaded via CDN for typography.

There is no backend, no database, and no build step.

---

## Getting started

The live, hosted version is available at:

**https://nazat02.github.io/QUANTA/**

Because QUANTA has zero dependencies and no build process, running it locally only requires opening the file:

```bash
git clone https://github.com/nazat02/QUANTA.git
cd QUANTA
open index.html      # macOS
# or
start index.html     # Windows
# or just double-click index.html / simulation.html in a file explorer
```

For a smoother local experience (avoiding browser quirks with local file access), it can also be served with any static file server:

```bash
# Python
python3 -m http.server 8000

# Node
npx serve .
```

Then visit `http://localhost:8000` and navigate to `simulation.html`, or use the **Observe Now** link from the landing page.

---

## Project structure

```
QUANTA/
├── index.html        # Marketing / landing page — explains the concept and links to the app
├── simulation.html   # The Quantum State Clock application
└── LICENSE            # MIT License
```

Everything — markup, styles, and logic — lives inline in the two HTML files, keeping the project portable and easy to read top to bottom.

---

## How it works (technical overview)

1. On load, `simulation.html` seeds a cloud of particles (or a Gaussian field, or a 3D shell, depending on the active mode) representing an unobserved superposition state.
2. The cloud animates continuously via a `render()` loop driven by `requestAnimationFrame`.
3. An **observation** is triggered by:
   - Clicking the **Observe** button or the canvas itself
   - Pressing `Space`
   - Returning to the tab (`visibilitychange`), refocusing the window (`focus`), or the page being shown again (`pageshow`) — each debounced so a single "look" doesn't trigger multiple collapses
4. On observation, the current system time is read and converted into target angles/positions (`timeToAngles`), and the cloud animates into three labelled spikes — hours, minutes, seconds — each in a distinct hue.
5. After a short hold, the state **decoheres**: the spikes dissolve back into the probability cloud, and the system returns to "superposition · unobserved" until the next observation.

---

## Browser support

QUANTA uses standard, broadly-supported web APIs (Canvas 2D, `requestAnimationFrame`, Page Visibility API, pointer/touch events) and runs in any modern evergreen browser — Chrome, Firefox, Safari, and Edge, on both desktop and mobile.

---

## License

This project is licensed under the **MIT License** — see [`LICENSE`](LICENSE) for details.

Copyright © 2026 Md. Shaikhul Hadis Nazat

---

## Contributing

Issues and pull requests are welcome. Since the entire app lives in two self-contained HTML files, contributions are easy to test — open the file in a browser and refresh.

New visualization modes, themes, or interactions should start with an issue to discuss the idea.
