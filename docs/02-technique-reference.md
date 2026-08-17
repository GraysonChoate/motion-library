# Technique Reference — demo values vs ship values

Open `ember-bench.html` in any browser to feel each technique. This file is the
index, and it exists mainly to answer one question:

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
| REV-03 | The Ratio | cream lerp | 0.08 | **0.08** | ✅ ship as-is — the pour should feel slow |

**Read the ✅ rows as the useful signal:** reveals and staggers were already tuned
for production. It's **depth, velocity and force** that got cranked for the demo —
DEP-01 travel, COP-02 skew, REA-01 repulsion, REA-02 magnetism. Those four are the
ones to dial back before shipping.

---

## Index

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

- **COP-01 · Character blur-stagger** — split to chars, animate from
  `blur + brightness(0) + translateY`. **Set `aria-label` on the parent** — splitting
  destroys the accessible string. Use CSS transitions, not rAF; the GPU handles it.
- **COP-02 · Velocity skew & settle** — reads scroll velocity, each line chases at its own
  rate. ⚠️ **The bug worth knowing: never lerp toward an already-decaying value.**
  Double-damping cost ~80% of amplitude. Accumulate, decay once.
  The effect lives in the **per-line rate difference**, not the skew.
- **COP-03 · Sticky set swap** — four-stop `mapStops` interpolation, top half drifts up
  while bottom drifts down. Move both the same way and it's just a slide.

### Group 04 — Reveal
How content arrives. Wipes and apertures instead of the universal fade-up.

- **REV-01 · Gradient mask wipe** — rewrite `mask-image` per frame. Flip axis to
  `to bottom` under 768px. Requires `will-change: mask-image` or Safari repaints the world.
- **REV-02 · Aperture open** — `clip-path: inset(50%)` → `0` on a Newton-Raphson-solved
  bezier. Clips a *container*, so parallax planes inside arrive as one world.
  `round 3px` stops the edge looking laser-cut.
- **REV-03 · The Ratio** — client-specific signature interaction. Cream floods via
  gradient mask; stage colour temperature travels with it. Built from `<button>`s, so it's
  keyboard-operable and announces state.

---

## The architecture that matters more than any effect

```js
// ONE loop for everything
const stages = new Map();
const io = new IntersectionObserver(es => es.forEach(e => {
  const s = stages.get(e.target); if (s) s.visible = e.isIntersecting;
}), { rootMargin: '120px' });

function loop(){
  stages.forEach(rec => { if (rec.visible && rec.tick) rec.tick(); });
  requestAnimationFrame(loop);
}
```

Eleven effects, one `requestAnimationFrame`, nothing computed off screen. Eleven
private loops would idle the page at 100% CPU. **Copy this pattern before you copy
any single effect.**

## Non-negotiables for anything shipped from here

1. `prefers-reduced-motion` fallback — every demo in the bench has one; keep them.
2. `aria-label` on any split text.
3. `will-change` on anything animating `mask-image`, `clip-path`, or `filter`.
4. Visible `:focus-visible` on every interactive control.
5. Clamp every input **before** mapping it, never the output after.
6. Mobile: re-check axis-dependent effects (mask wipes, horizontal parallax) — a
   horizontal wipe on a single-column phone layout reveals nothing.
