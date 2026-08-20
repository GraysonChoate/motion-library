# Standards — the tolerances

The floor. Anything shipped from this toolroom clears all of it.

---

## 1. Demo values are not ship values

Everything in [`TOOLROOM/TOOLROOM-UPLOAD-THIS.html`](../TOOLROOM/TOOLROOM-UPLOAD-THIS.html) is tuned
so the effect is **obvious at a glance** — visible in a still screenshot, unmistakable on
first hover. Production wants the opposite: the page feels alive and the reader **never
notices the mechanism**.

**Ship values run roughly 40–50% of demo values.** Per-constant table in
[`effects/README.md`](../effects/README.md).

> **The test: if a colleague can describe what the animation did, it's too strong.**

The four that most need dialling back — depth travel, velocity skew, particle repulsion,
magnet pull. Reveals and staggers were already tuned for production; ship those as-is.

---

## 2. One loop, gated

```js
const stages = new Map();
const io = new IntersectionObserver(es => es.forEach(e => {
  const s = stages.get(e.target); if (s) s.visible = e.isIntersecting;
}), { rootMargin: '120px' });

function loop(){
  stages.forEach(rec => { if (rec.visible && rec.tick) rec.tick(); });
  requestAnimationFrame(loop);
}
```

**One `requestAnimationFrame` for the whole page. Every animated section gated by an
`IntersectionObserver` so nothing off screen computes.** Eleven private loops will idle a
page at 100% CPU.

Anything added to `effects/` must register through the shared loop. A technique that
ships its own `requestAnimationFrame` doesn't go in.

---

## 3. Performance

- **Animate `transform` and `opacity` only** where possible — they're compositor-only.
  Animating `top`, `left`, `width`, `height` forces layout every frame.
- **`will-change`** on anything animating `mask-image`, `clip-path`, or `filter`.
  Without it Safari repaints the world.
- **Separate reads from writes.** Batch every `getBoundingClientRect` before any style
  write. Interleaving them forces synchronous layout each frame — this is the actual
  cause of most "why is my scroll animation janky."
- **Passive listeners** on `scroll`, `wheel`, `touchmove`: `{ passive: true }`.
- **Clamp inputs before mapping**, never outputs after.
- **`content-visibility: auto`** on long offscreen sections.
- **Cap particle counts** and scale them to viewport area.

---

## 4. Accessibility

- **`prefers-reduced-motion` is a designed state, not a kill switch.** Turning effects
  off leaves a dead page. Design the deliberate static composition — what does this
  section look like when nothing moves? That's also the honest answer for vestibular
  disorders, which large-field parallax genuinely triggers.
- **`aria-label` on any split text.** Splitting a headline into `<span>` per character
  destroys the accessible string; set the label on the parent and `aria-hidden` the
  pieces.
- **Visible `:focus-visible`** on every interactive control. Never `outline: none`
  without a replacement.
- **Real controls.** Buttons are `<button>`. State is announced — `aria-pressed`,
  `aria-expanded`. A styled `<div>` is not a control.
- **Contrast holds during motion.** Text mid-blur or mid-fade still has to be readable at
  every frame it's legible in.
- Respect `prefers-reduced-transparency` and `prefers-contrast` where you've leaned on
  either.

---

## 5. Mobile

- **Re-check axis-dependent effects.** A horizontal mask wipe on a single-column phone
  layout reveals nothing — flip to vertical under 768px.
- **Pointer effects need a touch story.** Tilt, magnetism and cursor-followers do nothing
  on a phone. Either provide a device-orientation equivalent or design the static state.
- **Halve particle counts and blur radii.** Blur is expensive on mobile GPUs.
- Test on a real mid-range device, not a desktop window resized narrow.

---

## 6. Typography

- **Font loading must not shift layout.** `font-display: swap` plus `size-adjust`,
  `ascent-override` and `descent-override` on the fallback so metrics match.
- Running text at **62–68 characters**; `text-wrap: balance` on headings.
- Uppercase labels get letter-spacing; tabular figures (`font-variant-numeric:
  tabular-nums`) wherever digits line up in columns.

---

## 7. Concept work

Unsolicited concept work is normal practice, with rules:

1. **Label it in the page** — visible and persistent, so nobody can mistake it for live.
2. **Invent nothing.** No prices, reviews, testimonials, credentials, claims or links you
   haven't verified.
3. **Carry the ®** on registered marks.
4. **Never imply a relationship that doesn't exist.**

---

## Checklist before anything ships

- [ ] Ship values, not demo values
- [ ] One rAF loop, all sections gated
- [ ] `prefers-reduced-motion` has a designed state, not a blank one
- [ ] Split text carries `aria-label`
- [ ] Every control keyboard-operable with visible focus
- [ ] Mobile: axis-dependent effects re-checked, pointer effects have a fallback
- [ ] No layout thrash — reads batched before writes
- [ ] Fonts don't shift layout on load
