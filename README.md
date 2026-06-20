# 🌑 Solar System · Eclipse Predictor

A real-time **gravitational N-body simulation** of the Solar System that derives planetary
orbits from first-principles physics and uses them to **predict solar eclipses** — then lets you
**stand on Earth and watch one happen**.

> 物理推導的行星軌道，即時推算日食，並可進入地球表面觀測日全食。

**▶ Live demo: https://solar-system-eclipse.vercel.app**

Inspired by the Claude Fable 5 demo *"simulates the solar system and predicts a solar eclipse."*
Single self-contained `index.html` — no build step.

---

## ✨ Features

- **Real gravity, not faked orbits.** Every body moves under `F = G·m₁·m₂/r²`, integrated with a
  symplectic velocity-Verlet integrator. Orbital periods, ellipses and perturbations *emerge* from
  the physics (energy is conserved to ~10⁻¹⁵ over years of simulated time).
- **Physically-derived eclipse forecast — solar *and* lunar.** The Moon's 5.14°-inclined orbit is
  perturbed by the Sun, so its nodes regress (~18.6 yr) and **eclipse seasons emerge on their own**
  (solar at new moon, lunar ~2 weeks later at full moon). Found by integrating the model forward and
  classified from the Moon's live distance: solar **Total / Annular / Hybrid / Partial**, lunar
  **Total / Partial / Penumbral**.
- **Lunar eclipses too.** Earth's shadow cone (umbra + penumbra) is rendered in 3D; from the surface
  you watch the full Moon slide into Earth's shadow and turn a coppery **"blood moon"** at totality.
- **🗺 Totality path (全食帶).** The Moon's umbra is projected onto a rotating Earth (obliquity +
  sidereal spin) to draw the narrow ground track of totality — *where you'd have to stand*.
- **Saros cycle explorer.** Step ±1 Saros (18 yr 11 d) and watch a series unfold: dates drift +11 days,
  the path marches ~⅓ of the globe west, gamma migrates across the node, and the type evolves
  (Annular → Hybrid → …). Includes an honest accuracy readout — the engine's Saros period vs the real
  6585.32 d — since a point-mass N-body is not a JPL-grade ephemeris.
- **🔭 Best-viewing predictor.** Next **opposition** for the outer planets (closest, brightest, up all
  night — flags Mars' rare "great opposition") and **greatest elongation** for Mercury/Venus (morning vs
  evening star), with date, distance and an estimated apparent magnitude — all from the live geometry.
- **Cinematic 3D rendering.** Three.js with real NASA-style planet textures, day/night terminators,
  a procedural granulating Sun, bloom, Saturn's ring, Earth's clouds + atmosphere, a Milky-Way
  backdrop and HUD labels that track each planet.
- **🌍 Enter Earth.** Click the Earth (or the globe button) to drop onto the surface and watch the
  eclipse unfold — for a solar eclipse the Moon crossing the Sun, sky darkening, corona and diamond
  ring; for a lunar eclipse the full Moon reddening into a blood moon — over a **sci-fi Egypt** horizon
  (glowing pyramids, light beam, holographic sands). Total vs. annular is decided by the Moon's real
  distance in the sim.
- **Responsive.** Adapts framing and HUD for desktop and mobile.

## 🎮 Controls

| Action | Control |
| --- | --- |
| Orbit camera | drag |
| Zoom | scroll / pinch |
| Play / pause | `space` or ⏸ |
| Step ±1 day | `←` / `→` |
| Jump to next eclipse | ⏭ |
| Enter Earth (surface view) | 🌍 button, or click the Earth |
| Time speed | slider |

## 🛠 Tech

- **Three.js r160** (WebGL) via ESM import-map — orbital scene, bloom post-processing, shaders
- **Canvas 2D** — the surface eclipse view and the node-geometry diagram
- **Vanilla JS** N-body engine (AU · days · solar-mass units, `G` = Gaussian *k²*)
- No framework, no bundler — just open `index.html`

## 🚀 Run locally

It's a single static file. Either open `index.html` directly, or serve it:

```bash
npx serve .
# then open http://localhost:3000
```

> Note: planet textures and Three.js are loaded from a CDN, so an internet connection is required.

## 🔬 How the eclipse prediction works

1. Initialise Sun + 8 planets on circular orbits and the Moon on an inclined orbit; integrate gravity.
2. Each step, compute the Moon's geocentric elongation from the Sun and its ecliptic latitude.
3. A **new moon** is a conjunction (elongation → 0); it's a **solar eclipse** when the Moon's
   latitude is small enough that the lunar shadow can reach Earth.
4. Because the Sun perturbs the tilted lunar orbit, eclipses naturally cluster into seasons ~6 months
   apart and drift earlier each year — exactly as they do in reality.

## 🙏 Credits

- Planet & Moon textures from [jeromeetienne/threex.planets](https://github.com/jeromeetienne/threex.planets)
- Built with [Three.js](https://threejs.org) · deployed on [Vercel](https://vercel.com)
- Created with [Claude Code](https://claude.com/claude-code)
