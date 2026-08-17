# Effects — the fixtures

Working, debugged interaction code. Lift it, keep the constants, swap the palette tokens.

Open [`effects-library.html`](effects-library.html) in any browser to feel each
technique. This file is the index, and it exists mainly to answer one question:

> **The demos look dramatic. Do I ship those numbers?**

**No.** Every constant in the bench is tuned for *legibility in a single glance* —
so the effect is obvious in a screenshot and on first hover. Production values are
tuned for the opposite: **the reader should feel the page is alive and never notice
the mechanism.** Ship the right-hand column.

Rule of thumb: **ship values are roughly 40–50% of demo values.** If a colleague
can describe what the animation did, it's too strong.

---

## The dial table

| ID | Technique | Constant | Demo | **Ship** | Why the gap |
|---|---|---|---|---|---|
| DEP-01 | Multi-plane parallax | near-plane travel | 150px | **60–80px** | 150px is visible in a still; 70px reads as depth without swimming |
| DEP-01 | | rotation × depth | 2.2° | **0.5–1°**, or 0 | rotation is the first thing that looks "effecty" |
| DEP-01 | | scroll travel | 150px | **70–90px** | keep under the plane's own inset or edges show |
| DEP-01 | | pointer lerp | 0.07 | **0.06–0.08** | ✅ ship as-is |
| DEP-02 | Tilted panel | rotateY max | 6° | **3–4°** | past 4° it reads as a toy |
| DEP-02 | | rotateX max | −5° | **−2.5 to −3°** | vertical tilt reads stronger than horizontal |
| DEP-03 | Focus falloff | blur per unit distance | 5px | **2.5–3px** | 5px is unreadable on real product imagery |
| DEP-03 | | opacity falloff | 0.34 | **0.2** | don't lose the off-focus items entirely |
| REA-01 | Ember field | particle count | area/9000, cap 150 | **area/14000, cap 90** | halve it on real pages; nobody counts embers |
| REA-01 | | repulsion force | 0.9 | **0.35–0.5** | 0.9 visibly blasts a hole |
| REA-01 | | repulsion radius | 120px | **90–110px** | ✅ near ship |
| REA-02 | Spark trail | spawn velocity gate | 4px | **6–8px** | higher gate = quieter, only rewards intent |
| REA-02 | | spark cap | 260 | **120** | trails are cheap until they aren't |
| REA-02 | Magnetic control | pull factor | 0.28 | **0.14–0.18** | above 0.2 the button dodges the cursor |
| REA-02 | | radius | 150px | **110–130px** | ✅ near ship |
| COP-01 | Char blur-stagger | stagger | 0.015s | **0.012–0.018s** | ✅ ship as-is |
| COP-01 | | initial blur | 10px | **6–8px** | 10px on long headlines delays legibility |
| COP-02 | Velocity skew | skew multiplier | −0.11 (±14°) | **−0.035 (±4–5°)** | **biggest gap in the library** — 14° is a demo only |
| COP-02 | | vertical drag | 0.34 | **0.10–0.15** | drag is what fights readability most |
| COP-02 | | blur multiplier | 0.05 (max 5px) | **0.02 (max 1.5–2px)** | never blur text a user is reading |
| COP-02 | | per-line rates | .22/.15/.10 | **.20/.16/.13** | keep the *spread*, tighten the range |
| COP-02 | | input clamp | ±130 | **±90** | ✅ near ship |
| COP-03 | Sticky set swap | blur in/out | 15px | **10–12px** | ✅ near ship |
| COP-03 | | opposing drift | 120px | **70–90px** | ✅ near ship |
| REV-01 | Mask wipe | lead % | 130% | **130%** | ✅ must exceed 100% to fully clear |
| REV-01 | | edge softness | 15% / 20% mobile | **same** | ✅ ship as-is |
| REV-02 | Aperture open | ease | cubic(.65,0,.35,1) | **same** | ✅ ship as-is |
| REV-03 | Proportional fill | fill lerp | 0.08 | **0.08** | ✅ ship as-is — the pour should feel slow |
| REV-04 | Sticky stacking | buried scale-down | 0.10 | **0.06–0.08** | too much and buried cards vanish |
| REV-04 | | buried dim | 0.55 | **0.35–0.45** | ✅ near ship |
| REV-05 | Progressive blur | max layer blur | 26px | **14–18px** | 26px eats the content behind it |
| REV-05 | | layer count | 4 | **3–4** | ✅ fewer than 3 and the seam shows |
| SYS-01 | CSS scroll timeline | animation-range | entry 10% cover 55% | **same** | ✅ tune to content, not to taste |
| SYS-02 | FLIP | transition | .55s cubic(.2,.8,.2,1) | **.35–.45s** | layout moves should feel quick |
| SYS-03 | Spring | stiffness K | 0.10 | **0.08–0.12** | ✅ ship as-is |
| SYS-03 | | damping D | 0.72 | **0.75–0.80** | 0.72 overshoots visibly; fine for a demo |
| TYP-02 | Line mask | per-line stagger | 0.07s | **0.05–0.08s** | ✅ ship as-is |
| TYP-03 | Tracking open | final tracking | 0.22em | **0.12–0.18em** | past 0.25em it stops being a word |
| TYP-04 | Weight response | falloff radius | 190px | **130–160px** | wide radius makes the whole line move |
| TYP-04 | | weight travel | 300→700 | **300→600** | ✅ near ship |
| TYP-05 | Scramble | duration | 1400ms | **900–1200ms** | long scrambles delay reading |
| TYP-06 | Counter roll | per-digit delay | 0.06s | **0.04–0.06s** | ✅ ship as-is |
| TYP-09 | Velocity marquee | idle drift | 0.4px/f | **0.25–0.4** | ✅ ship as-is |
| TYP-09 | | scroll coupling | 0.35 | **0.15–0.25** | 0.35 whips hard on trackpads |
| AMB-01 | Animated grain | regen interval | 80ms | **80–120ms** | ✅ ship as-is — faster is invisible |
| AMB-01 | | opacity | .09 (demo) | **.03–.05** | demo is 2× so it reads in a screenshot |

**Read the ✅ rows as the useful signal:** reveals and staggers were already tuned
for production. It's **depth, velocity and force** that got cranked for the demo —
DEP-01 travel, COP-02 skew, REA-01 repulsion, REA-02 magnetism. Those four are the
ones to dial back before shipping.

---

## Index

### Group 00 — Architecture (`SYS-`)
Read first. These change how everything after them is built.

- **SYS-01 · Native CSS scroll timelines** — `animation-timeline: view()`. Zero JS, runs
  off the main thread, physically cannot jank. **Reach for this before writing any scroll
  JS.** Wrap in `@supports`; degrades to no animation.
- **SYS-02 · FLIP** — measure, mutate, invert, release. The only way to animate real layout
  change at 60fps. **The most important technique here and the one fewest people know.**
- **SYS-03 · Spring physics** — no duration; integrates position and velocity, so
  interruptions carry momentum. Tune stiffness and damping, not duration.

### Group 0.5 — Rendered (`GL-`)
The GPU tier. All **raw WebGL2 — still zero dependencies.**

- **GL-01 · Raymarched SDF field** — geometry as a distance function. Domain repetition gives
  infinite grids for free. Cost is per-pixel, not per-object. Watch DPR on mobile.
- **GL-02 · Dispersion glass** — R/G/B refracted at different IOR, which is what makes real
  glass fringe. Refract all three identically and it's just a blurry circle.
- **GL-03 · Displacement transition** — two textures blended through a noise map. **The
  character comes entirely from the noise**, not the blend.
- **GL-04 · Fluid cursor** — ping-pong FBOs. Two framebuffers swapping roles each frame is the
  general pattern for *any* GPU simulation.

⚠️ This is **the one group permitted a library** in production (Three.js). That permission
does not extend anywhere else. Everything here also needs a static fallback — the demos
degrade to a printed message when WebGL2 or float framebuffers are unavailable.

### Group 04.5 — Platform (`PLT-`)
Not effects — new browser powers, several of which delete code we currently write.

- **PLT-01 · `interpolate-size`** — animating height to `auto`. Kills every max-height hack.
- **PLT-02 · `@starting-style`** — entry animations for elements that didn't exist yet.
  Replaces the double-rAF dance. Pairs with `transition-behavior: allow-discrete`.
- **PLT-03 · Popover + anchor positioning** — top layer, light-dismiss, Esc and focus for free.
  **Replaces Floating UI and ends the z-index war.** Anchor positioning is Chromium-only — guard it.
- **PLT-04 · `@property`** — typed custom properties make **gradients and angles animatable**.
- **PLT-05 · Container queries** — components responding to their own width, not the viewport.
- **PLT-06 · Scroll-snap events** — `scrollsnapchange` / `scrollsnapchanging`. The browser
  already knows which item snapped.

Every one needs an `@supports` guard and a **designed** fallback.

### Group 01 — Depth
Making flat surfaces into space you move through.

- **DEP-01 · Multi-plane parallax** — the highest-value technique here. Five planes,
  each translating by `depth × pointer` and `depth × scroll`.
  **Parallax only reads if all three are true:** silhouettes that occlude each other,
  enough travel, and blur on the nearest plane. Two out of three looks flat.
  Includes an exploded **Show planes** view for teaching.
- **DEP-02 · Pointer-tilted panel** — `perspective` on parent, `rotateX/Y` on child.
  The small accompanying `translate` is what sells it; pure rotation feels hinged.
  Never tilt running text.
- **DEP-03 · Focus falloff** — a virtual focal plane driven by pointer X. Blur +
  brightness + scale together; any one alone reads flat. Cheaper than parallax
  because nothing travels far.

### Group 02 — Reactivity
The category video cannot compete in.

- **REA-01 · Ember field with pointer wake** — canvas particles, `globalCompositeOperation
  = 'lighter'` for glow, linear falloff repulsion. Scale count to viewport area and cap it.
- **REA-02 · Spark trail + magnetic control** — trail spawns on **velocity**, not on every
  pointer event. `Array.filter` doubles as the cleanup pass. Magnetism belongs on exactly
  one control per page.

### Group 03 — Copy in motion
Type moves to carry hierarchy and consequence, never to be seen moving.

- **TYP-02 · Line mask reveal** — clip per line, rise it in. **The correct reveal for
  anything longer than a headline** — char stagger on body copy delays legibility.
- **TYP-03 · Tracking open** — letter-spacing as the animation; nothing translates.
- **TYP-04 · Weight response** — per-character weight by pointer distance. With a real
  variable font this drives `font-variation-settings: 'wght'` continuously.
- **TYP-05 · Text scramble** — glyphs resolve left to right. Set `aria-label`.
- **TYP-06 · Counter roll** — digit strips translated by `-Nem`. Requires `tabular-nums`.
- **TYP-09 · Velocity marquee** — speed *and direction* follow scroll velocity.
- **TYP-01 · Character blur-stagger** — split to chars, animate from
  `blur + brightness(0) + translateY`. **Set `aria-label` on the parent** — splitting
  destroys the accessible string. Use CSS transitions, not rAF; the GPU handles it.
- **TYP-07 · Velocity skew & settle** — reads scroll velocity, each line chases at its own
  rate. ⚠️ **The bug worth knowing: never lerp toward an already-decaying value.**
  Double-damping cost ~80% of amplitude. Accumulate, decay once.
  The effect lives in the **per-line rate difference**, not the skew.
- **TYP-08 · Sticky set swap** — four-stop `mapStops` interpolation, top half drifts up
  while bottom drifts down. Move both the same way and it's just a slide.

### Group 04 — Reveal
How content arrives. Wipes and apertures instead of the universal fade-up.

- **REV-01 · Gradient mask wipe** — rewrite `mask-image` per frame. Flip axis to
  `to bottom` under 768px. Requires `will-change: mask-image` or Safari repaints the world.
- **REV-02 · Aperture open** — `clip-path: inset(50%)` → `0` on a Newton-Raphson-solved
  bezier. Clips a *container*, so parallax planes inside arrive as one world.
  `round 3px` stops the edge looking laser-cut.
- **REV-03 · Proportional fill** — a discrete control floods a fill and travels the stage's
  colour temperature. Signature-interaction slot. Built from real `<button>`s.
- **REV-04 · Sticky stacking cards** — cards pile in one sticky viewport; buried ones scale
  down and dim. The scale-down is what sells depth.
- **REV-05 · Progressive blur** — layered `backdrop-filter` with overlapping gradient masks.
  **One masked blur layer produces a visible seam** — softness comes from the overlap.

### Group 05 — Ambient (`AMB-`)
Noticed only in its absence.

- **AMB-01 · Animated film grain** — canvas noise regenerated at ~12fps, half resolution,
  `mix-blend-mode: overlay`. Kills gradient banding.

---

## Before you ship any of this

Two things live in [`../standards/`](../standards/) and apply to everything here:

**One `requestAnimationFrame` loop for the whole page**, every section gated by an
`IntersectionObserver`. Anything added to this folder must register through the shared
loop — a technique that ships its own rAF doesn't go in.

**The full accessibility and performance floor** — reduced-motion as a designed state,
`aria-label` on split text, `will-change` on masks and filters, reads batched before
writes, mobile axis checks. Run the checklist at the bottom of
[`../standards/README.md`](../standards/README.md).

---

## Adding a technique

Keep the shape: a `<div class="stage" data-demo="…">` with a live demo, a rail stating
**what it does** and **when to use it**, and a `<details>` code block with the tuned
constants highlighted. Register through `register(stage, init)`.

Give it an ID in an existing group, and add a row to the dial table above with **both**
demo and ship values.

| Prefix | Group | Purpose |
|---|---|---|
| `DEP-` | Depth | flat surfaces into space you move through |
| `REA-` | Reactivity | the page answering pointer and input |
| `SYS-` | Architecture | motion systems that change how you build |
| `GL-` | Rendered | GPU / shader work — the one group allowed a library |
| `PLT-` | Platform | new browser capability, not effects |
| `TYP-` | Typography | type as the subject, not the vehicle |
| `REV-` | Reveal | how content arrives |
| `AMB-` | Ambient | atmosphere, grain, idle life |

### Backlog

Built as of this version: **34 techniques across eight groups.** Still queued —

**Architecture** — View Transitions API (`view-transition-name`) · Speculation Rules
(prefetch on hover intent, pairs with View Transitions for app-like navigation)

**Typography** — text on a curved path (SVG `textPath`) · knockout type
(`background-clip: text`) · optical-size axis switching

**Rendered** — GPGPU particles (positions in textures) · post-processing stack (bloom, DOF,
chromatic aberration) · mesh distortion on scroll · **Gaussian splatting** and **MSDF text**,
both of which need real asset files and a local build rather than a single HTML page

**Depth** — depth-map 2.5D displacement · sticky scale-through · device-orientation tilt
for mobile

**Reactivity** — cursor lens / local magnification · custom cursor with state morph ·
elastic drag with momentum · RGB split on hover · pointer-reactive mesh

**Reveal** — curtain and split transitions · staggered grid entrance

**Ambient** — slow noise field · breathing on idle

Everything currently in `GL-` is raw WebGL2 with no dependencies. The queued splatting and
MSDF items genuinely need asset files, so they belong in a local project rather than this
single self-contained page.

Two constraints: **no dependencies**, and it must register through the shared loop.
