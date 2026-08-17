# Motion Library

A working reference for building **reactive, dimensional websites for local
businesses** — cafés, studios, gyms, restaurants, salons, small retail. Two halves:

1. **A live motion bench** — eleven scroll and pointer techniques you can feel and copy.
2. **A research playbook** — how to gather real brand facts before designing anything.

Built with **no dependencies, no build step, and no video or image assets.**

---

## Start here

| I want to… | Go to |
|---|---|
| **I'm new here** | **[`docs/00-intern-handoff.md`](docs/00-intern-handoff.md) — start here** |
| **Feel the techniques** | Open `motion-bench.html` in any browser. Move your cursor into each stage. |
| **Copy a technique into a project** | [`docs/02-technique-reference.md`](docs/02-technique-reference.md) — ⚠️ read the demo-vs-ship table first |
| **Research a new client properly** | [`docs/01-research-playbook.md`](docs/01-research-playbook.md) |
| **Do the research on a client** | [`templates/research-card.md`](templates/research-card.md) — the fill-in deliverable |

> **Status: unvalidated, v1.** The research half has been run once on a real client.
> The build half has never been run. Nobody has yet taken research from this process
> through to a finished page, so **there is no evidence this produces better work than
> taste would have.** Treat it as a hypothesis to test, not a method to trust.

`motion-bench.html` is a single self-contained file. Double-click it. No install,
no server, no npm.

### Where this lives, and how to move it

This folder currently sits inside the `grounded-labs-website` repo purely for lack of
somewhere better — it is **unrelated to the Grounded Labs project** and touches none of
it. It was meant to be its own repo, but the automation creating it lacked
repo-creation permission.

It is **fully self-contained and portable**. To give it a proper home:

```bash
mkdir motion-library && cd motion-library
cp -r /path/to/grounded-labs-website/motion-library/. .
git init && git add -A && git commit -m "Motion Library"
# then create an empty repo on GitHub and:
git remote add origin git@github.com:<you>/motion-library.git
git push -u origin main
```

Nothing references a path outside this folder, so the copy works as-is.

---

## ⚠️ Read this before shipping anything

**The bench is tuned for demo legibility, not production.** Constants are cranked so
each effect is obvious in a single glance and visible in a screenshot. Production wants
the opposite: the page feels alive and the reader **never notices the mechanism**.

**Ship values are roughly 40–50% of demo values.** The full dial table is in
[`docs/02-technique-reference.md`](docs/02-technique-reference.md). The four that most
need dialling back:

| Technique | Demo | Ship |
|---|---|---|
| DEP-01 near-plane travel | 150px | **60–80px** |
| COP-02 skew | ±14° | **±4–5°** |
| REA-01 ember repulsion | 0.9 | **0.35–0.5** |
| REA-02 magnet pull | 0.28 | **0.14–0.18** |

Reveals and staggers (COP-01, COP-03, REV-01/02/03) were already tuned for production —
ship those as-is. If a colleague can describe what the animation did, it's too strong.

---

## What's in the bench

**Group 01 — Depth.** Flat surfaces into space you move through.
`DEP-01` multi-plane parallax (+ exploded "Show planes" view) ·
`DEP-02` pointer-tilted panel · `DEP-03` focus falloff

**Group 02 — Reactivity.** The category video cannot compete in.
`REA-01` ember field with pointer wake · `REA-02` spark trail + magnetic control

**Group 03 — Copy in motion.** Type moving to carry meaning, not to be seen moving.
`COP-01` character blur-stagger · `COP-02` velocity skew & settle ·
`COP-03` sticky set swap with opposing drift

**Group 04 — Reveal.** Wipes and apertures instead of the universal fade-up.
`REV-01` gradient mask wipe · `REV-02` aperture open · `REV-03` The Ratio (cream flood)

---

## The four ideas worth more than any single effect

**1. One loop, gated.** Eleven effects share a single `requestAnimationFrame`, and every
stage is registered with an `IntersectionObserver` so nothing off screen computes.
Eleven private loops would idle a page at 100% CPU. **Copy this pattern before you copy
any effect.**

**2. Depth ≠ arrival.** Things appearing on screen is not dimension. Dimension is
parallax *between* planes, focus falling off with distance, and light moving
independently of what it lands on. Parallax only reads when **all three** are true:
silhouettes that occlude each other, enough travel, and blur on the nearest plane.

**3. Input is the material.** Video can't answer the cursor. Every technique here reads
pointer or scroll and responds in the same frame — that is the whole difference between
alive and playing back.

**4. Steal mechanics, reject mood.** Reference builds carry a genre along with their
technique. A neural-tech scroll engine is reusable; its coldness on a coffee brand
produces "an AI startup that happens to sell lattes."

---

## The research half

Design decisions here come from **measured data, not taste**. The playbook exists
because, on the one client it has been run against, an unmeasured palette guess survived
three rounds of discussion before measurement disproved it. The guessed colour was not
even in the brand's palette. Nothing built on it would have been theirs.

Two things from [`docs/01-research-playbook.md`](docs/01-research-playbook.md) that
save the most time:

**Evidence tiers.** Tag every fact A–F, from *measured bytes* down to *my imagination*.
Never ship tier F. Mixing tiers is how a guess becomes a build spec.

**Route by source type.** Automated fetching works fine on a small business's own site
and fails completely on search engines and social platforms — datacenter IPs get bot
checks, empty JS shells, or unrelated junk. **Ask a human for those screenshots up front
instead of burning four attempts on a locked door.** One screenshot from a real browser
beat four automated attempts at Instagram.

Also non-negotiable: **measure palettes, never eyeball them** (ImageMagick on the
client's own images), and **sanity-check every image before measuring it** — an image
search once returned industrial V-belt product shots, the palette math ran perfectly,
and produced a completely fictitious brand palette. Correct arithmetic on wrong inputs
is more dangerous than an error, because nothing looks broken.

---

## Accessibility & performance floor

Anything shipped from here keeps all six:

1. `prefers-reduced-motion` fallback — every bench demo has one
2. `aria-label` on any split text (splitting destroys the accessible string)
3. `will-change` on anything animating `mask-image`, `clip-path`, or `filter`
4. Visible `:focus-visible` on every interactive control
5. Clamp inputs **before** mapping, never outputs after
6. Re-check axis-dependent effects on mobile — a horizontal wipe on a single-column
   phone layout reveals nothing

---

## Adding to the library

Keep the bench's shape: a `<div class="stage" data-demo="…">` with a live demo, a rail
stating **what it does** and **when to use it**, and a `<details>` code block with the
tuned constants highlighted. Register the demo through the shared
`register(stage, init)` helper so it joins the single loop and the visibility gate —
never add a second `requestAnimationFrame`.

Give it an ID in an existing group and add a row to the dial table in
`docs/02-technique-reference.md` with **both** demo and ship values.

Current groups — open a new prefix when something genuinely doesn't fit:

| Prefix | Group | Purpose |
|---|---|---|
| `DEP-` | Depth | flat surfaces into space you move through |
| `REA-` | Reactivity | the page answering pointer and input |
| `COP-` | Copy in motion | type carrying hierarchy and consequence |
| `REV-` | Reveal | how content arrives |
| `TYP-` | Typography | *open* — type as the subject, not the vehicle |
| `AMB-` | Ambient | *open* — atmosphere, grain, idle life |

### Backlog

Candidates worth building next. Claim one by opening a PR.

**Typography (`TYP-`)** — variable-font weight driven by scroll or pointer distance ·
per-line mask reveal · letter-spacing that opens on scroll · type on a curved path ·
tabular counter roll-up · marquee with velocity-linked speed

**Depth (`DEP-`)** — 2.5D displacement from a depth map · sticky scale-through
transition · device-orientation tilt for mobile

**Reactivity (`REA-`)** — cursor lens / local magnification · hover displacement on
imagery · pointer-reactive grid or mesh

**Reveal (`REV-`)** — curtain and split transitions · staggered grid entrance ·
cross-page transition without a framework

**Ambient (`AMB-`)** — animated grain · slow noise field · breathing scale on idle

Two constraints for anything added: **no dependencies**, and it must register through
the shared loop. A technique that ships its own `requestAnimationFrame` or pulls in a
library doesn't go in.

---

## Palette

The bench is skinned in the **Grounded Labs palette** — graphite black, luminous ivory,
pale blueprint blue, warm gray, muted burnt orange, aged brass, restrained honey-gold.

**The palette is a skin, not a dependency.** Every technique is client-agnostic. Swap the
tokens in `:root` and the whole bench re-skins in one edit. Nothing in the library
references a specific client.
