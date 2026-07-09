# BRIEF: "NEON CHRONOS"

## Concept/Theme
**Digital Erosion / Cyber-Brutalism.**
The site is not a landing page; it is a simulation of data decay in a near-future interface. The user navigates a grid that slowly dissolves into noise and procedural distortion the longer they scroll (simulating time passing). It feels like hacking a terminal that is fighting to stay alive.

## Color Palette
- **Void**: `#050505` (Near black, almost pure)
- **Signal**: `#00F0FF` (Electric Cyan - for UI elements)
- **Warning**: `#FF2A00` (High-vis Orange - used sparingly for errors/damage)
- **Surface**: `#111111` (Slightly lighter black for depth)

## Typography
- **Headline**: `Space Grotesk` (Variable weight). Used for large, erratic, all-caps headers. Rationale: Its inherent digital/monospaced feel but with humanist curves fits the cyber-noir aesthetic better than raw monospace.
- **Data/UI**: `JetBrains Mono`. Strictly monospaced for that "code" feel, used strictly for micro-text and coordinates.

## Signature Technique
**Procedural WebGL Shaders (Three.js).**
A custom GLSL vertex/fragment shader drives a wireframe icosahedron mesh, displacing every vertex with 3D simplex noise whose amplitude scales with scroll depth — the further you scroll, the more the "memory" visibly corrupts. Fragment color interpolates from Signal cyan to Warning orange as displacement increases. Foreground headline text uses a CSS custom-property-driven RGB-split glitch effect, triggered on hover and randomly at increasing frequency as scroll depth (the "entropy" value) rises.

## Mood/Feeling (First 3 Seconds)
The user should feel **intruded upon**. The site starts "corrupted" — a boot sequence stutters across the screen, warning text flickers in, and the custom cursor (a ring that reacts to hoverable elements) replaces the system pointer entirely. There is no hero image, only shifting abstract geometry and floating data packets.

---
**Decision:** Three.js drives the background mesh (a distorted wireframe icosahedron) via a custom ShaderMaterial; CSS/SVG handles foreground typography and the noise-grain overlay to keep the mobile frame rate high while preserving visual fidelity. No external images — all textures/effects are procedural (GLSL noise, SVG feTurbulence, CSS gradients).
