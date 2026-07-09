# BUILD NOTES — NEON CHRONOS

## Concept
Cyber-brutalist "digital erosion" simulation: a single-page scroll narrative in which the site itself decays as the visitor scrolls. Scroll depth maps directly onto an `entropy` value (0–1) that drives every system on the page — a wireframe icosahedron's distortion, a scanline overlay, a corrupting live clock, and the rate of RGB-split glitch text.

## Signature Technique
A custom GLSL `ShaderMaterial` (vertex + fragment) on a Three.js icosahedron wireframe: 3D simplex noise displaces every vertex, with amplitude and color-mix both driven by the `uEntropy` uniform. No canned particle library, no post-processing pass — the distortion is hand-written noise math tied to a single scroll-derived value, reinforced by a corrupting HUD clock (digits randomly misfire as entropy rises) that literalizes the "Chronos" half of the concept.

## What changed across the 3 critique passes
1. **Pass 1 — structural/interaction bug + missing depth.** Found a CSS specificity bug where `body.touch-device` couldn't override `cursor: none` on the `.cta`/`.reboot` elements (two-class selector loses to the single-class rule), leaving mobile users with no visible cursor affordance. Fixed the override, and added a radial vignette layer for depth since the flat mesh-on-black felt shallow without adding an image asset.
2. **Pass 2 — concept gap.** The site is named for time ("Chronos") but nothing in the experience actually represented time — only scroll-driven entropy. Added a live elapsed-time HUD clock whose digits probabilistically corrupt in proportion to entropy, so the temporal-decay half of the concept actually lands instead of being implied only by the name.
3. **Pass 3 — pacing.** Sections were popping into view with no entrance choreography, flattening the rhythm between the four narrative layers. Added an IntersectionObserver-driven reveal (staggered opacity/translateY using the existing custom easing curves, not linear/ease-in-out) so each layer arrives with its own beat.

## Post-build QA catch (Step 5)
Puppeteer screenshots at full scroll depth revealed a real legibility failure: the shader's displacement amplitude and mesh alpha both *increased* with entropy, so by 100% scroll the wireframe became dense enough to swallow the "END OF LINE" copy — the exact moment the concept should be most readable. Fixed by capping displacement amplitude, inverting the alpha curve so the mesh gets subtler (not denser) as it corrupts, and adding a left-side scrim that darkens in step with entropy to protect the text column. Re-verified via screenshot at 0%, 66%, and 100% scroll on both desktop (1440×900) and mobile (390×844) — zero console errors at every stage.

## What I'd improve with more time
The glitch-text and scanline systems are convincing, but the "packet" point cloud in the background is static in shape — it would sell the decay concept harder if individual points also drifted/despawned in response to entropy (echoing "packet loss") rather than only rotating as a fixed field.

## Deploy status
Netlify deploy was not run — it's a live/production action outside what this turn explicitly authorized, so it was blocked by the permission layer. The site is served locally and verified working at **http://localhost:8080**. Say the word and I'll push it to Netlify for a public URL.
