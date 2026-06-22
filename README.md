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
- **🌐 Multilingual + Field Guide.** An in-app guide opens on every visit; pick **English / 中文 / 日本語**
  and the whole interface switches to that language.
- **🔭 Sky-events predictor.** Next **opposition** for the outer planets (closest, brightest, up all
  night — flags Mars' rare "great opposition") and **greatest elongation** for Mercury/Venus (morning vs
  evening star), with date, distance and an estimated apparent magnitude. Plus **conjunctions (合)** —
  close planet pairings (the ~20-yr Jupiter–Saturn "Christmas Star"), the Moon's monthly photogenic
  passes, and multi-planet **alignments (行星連珠)** — all from the live geometry (planets carry real
  orbital inclinations, so the on-sky separations are realistic).
- **Cinematic 3D rendering.** Three.js with real NASA-style planet textures, day/night terminators,
  a procedural granulating Sun, bloom, Saturn's ring, Earth's clouds + atmosphere, a Milky-Way
  backdrop and HUD labels that track each planet.
- **🌍 Pick your observing site.** Click the Earth to open an interactive **globe** — drag to rotate and
  tap to drop a pin anywhere, or browse **17 recommended cities grouped by continent** — pick a region
  (Asia · Europe · Africa · Americas · Oceania), then a city — which turns the globe to face that
  location. The continents (and a region's cities) are also **labelled directly on the 3D globe**, with
  labels that track the surface and hide round the far side as you rotate. The pin lands on the **real
  geographic position** on the Earth map (the lat/lon → sphere mapping matches the texture). Every
  eclipse calculation then runs **topocentrically from that point**: real lunar parallax (so the site
  sees its own total/partial/none), the **horizon** (the Sun may be below it — "not visible, it's
  night here"), and "the next eclipse visible *from here*." Your pin is also drawn on the totality-path
  map. (The *eclipse-engine* longitude frame is model coordinates, not tied to the map — see notes.)
- **🌍 Enter Earth — over a real photo of your city.** Drop onto the surface and watch the eclipse
  unfold over an **actual photograph of the place you chose** — the Giza pyramids, Paris with the
  Eiffel Tower, the Lower-Manhattan skyline, the Shinjuku skyscrapers, or Westminster — which **darkens
  toward an eerie twilight as totality nears**, with stars coming out and city lights switching on. The
  Sun's Moon-crossing, corona and diamond ring (or the reddening blood-Moon for a lunar eclipse) play
  out above the skyline, **oriented to that city's local horizon** (alt-az), so the angle at which the
  Moon bites into the Sun is the one you'd actually see standing there — a site near the central path
  sees a near-head-on cover, one far from it a slanted, shallow partial. Total vs. annular is decided
  by the Moon's real distance in the sim. (Any non-listed pin falls back to a drawn horizon.)
- **🪐 Tap any planet for an astronomer's fact sheet.** Click any of the 8 planets in the orbital view
  to open a dedicated viewer: that planet rendered as a slowly-rotating, axially-tilted globe (real
  NASA texture, Saturn's ring, Earth's clouds/atmosphere) beside a professional data panel — 10
  physical & orbital parameters (mass, mean density, surface gravity, semi-major axis, orbital &
  sidereal-rotation periods, obliquity, eccentricity, temperature), atmospheric composition, a set of
  notable features, and a detailed exploration history/outlook (curated to early 2026). Step through
  the planets with ‹ / › . (Earth's click still opens the observing-site globe.)
- **📡 Live Mission Feed + agency dossiers.** A 📡 panel with two tabs. **Live feed** pulls the
  **latest real space news** (aggregated across NASA, SpaceX, ESA and more via the Spaceflight News
  API) and the **next upcoming launches** with live countdowns (The Space Devs · Launch Library 2),
  filterable by NASA / SpaceX / ESA / China / Moon / Mars. A persistent **agency dock down the left edge**
  (and an **Agencies** tab in the panel) opens a cinematic, accent-themed
  **profile dossier** for each major organisation — NASA, ESA, SpaceX, Roscosmos, CNSA, JAXA, ISRO,
  Blue Origin, Rocket Lab — with a glowing emblem, the **official logo**, founding/HQ/type, a milestones
  timeline, **a gallery of historical mission photos with captions** (Wikimedia Commons), and current
  programs. A **Watch** tab embeds a curated set of **official @SpaceX clips, all under 10 minutes**
  (mission cinematics, Starship flight-test recaps, the EVA suit, Polaris Dawn & Fram2), each playing
  inline via the privacy-friendly youtube-nocookie player — a quick look at humanity's progress in space.
  (Live feeds fetched client-side and cached briefly; they degrade gracefully if unavailable.)
- **⏪ Reverse time.** Run the gravitational clock **backwards** as well as forwards — the symplectic
  integrator is time-reversible (energy holds to ~10⁻¹⁶ either way), so you can rewind orbits and the
  eclipse cycle. The ⏭ jump even finds the *previous* eclipse when time is reversed.
- **Responsive.** Adapts framing and HUD for desktop and mobile.

## 🎮 Controls

| Action | Control |
| --- | --- |
| Orbit camera | drag |
| Zoom | scroll / pinch |
| Play / pause | `space` or ⏸ |
| Reverse time direction | ⏪ |
| Step ±1 day | `←` / `→` |
| Jump to next / previous eclipse | ⏭ (follows time direction) |
| Planet fact sheet | click any planet |
| Enter Earth (surface view) | 🌍 button, or click the Earth |
| Live space news & agency profiles | 📡 |
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
