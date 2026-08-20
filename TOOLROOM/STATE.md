# TOOLROOM — CURRENT STATE

**Last updated 2026-08-20.** Written for picking up cold. Read this before touching anything.

---

## What this is

The Grounded Labs Toolroom: one self-contained HTML file that turns any AI into a
website-elevating agent. Upload it to a fresh chat, send `IMPLEMENT PHASE ONE — <url>`,
get a homepage concept back as a **link** in about twenty minutes.

## Where it lives

| | |
|---|---|
| **Canonical file** | `TOOLROOM/TOOLROOM-UPLOAD-THIS.html` in `GraysonChoate/motion-library`, branch `claude/sculpt-glow-foundation-prep-w5g1ms` |
| **Raw download** | `https://raw.githubusercontent.com/GraysonChoate/motion-library/claude/sculpt-glow-foundation-prep-w5g1ms/TOOLROOM/TOOLROOM-UPLOAD-THIS.html` |
| **Artifact** | `https://claude.ai/code/artifact/b5dc9473-a0f7-4658-82f5-1495fa86af65` — **may be stale, see divergence below** |
| **Version** | `2026-08-20 · v8` — stamped at byte zero AND on the front door. Check it before trusting any copy. |

Nothing else in the repo goes into a build chat. `HANDOFF.md` is for a session that EDITS
the Toolroom. `builds/` is output. Anything named `*-FIX-PROMPT.md` or `RETROSPECTIVE-*.md`
is a document ABOUT the tool — feeding one to a build chat makes the AI edit the Toolroom
instead of building a website. That has already happened.

## State as of this pause

- **35 mechanical checks.** 53 effects in 9 groups. Seven tabs plus a three-door front end.
- Verified: zero page errors across every mode, tab and sub-tab; doors, tabs, sub-tabs, all
  53 gallery cards and the floating Back control confirmed hit-testable by **real pointer
  input** (not `element.click()`); no horizontal overflow; both embedded code blocks pass
  `node --check` after extraction.

---

## UNRESOLVED — read before you edit

### 1. The artifact and git have diverged, and the merge report did not verify

Another session reported making 28 edits (a STEP 0 sight gate, BLD 05a, IMAGERY as step 6,
an AMPLIFY verdict, renumbering to eleven steps, checks 32–35) and republishing to the same
artifact URL. **The file Grayson later downloaded was byte-identical to commit `43db59d` —
my own version, MD5 match, containing none of those edits.** Either the republish never
landed or the wrong copy was fetched. Their work has never been pushed to git and is not
recoverable from here.

**I rebuilt the most valuable part myself** — STEP 0, BLD 05a and the nine-rung ladder are
now in v8. So the sight gate is covered.

**Numbering has diverged permanently.** Mine: 32/33 = vanished content + collapsed
container, 34/35 = provenance. Theirs used 32–35 for different checks. If their file ever
surfaces this is a manual reconcile, not a merge.

**Untried next step:** `WebFetch` claims `claude.ai/code/artifact/{uuid}` URLs *are*
fetchable with a claude.ai login — unlike `curl`, which gets a Cloudflare 403. I never
tried it. That could settle this in one call.

### 2. No genuine cold test has ever been run

The document has been fixed a great deal and proven once. A clean test was being set up at
this pause — local session, `~/Documents/Grounded Labs`, `CLAUDE.md` temporarily renamed to
`CLAUDE.md.off` so the motion-project brief doesn't contaminate it. **Put that back after.**

---

## OPEN WORK, in priority order

### 1. The materials chapter — the biggest real gap

KIT 10 says **which** material a register calls for (Raw→worn metal, Craft→wood/suede,
Community→sand/canvas) and which materials each trade uses. It never says **how to make
one.** Every recipe resolves to mesh-gradient blobs plus film grain, which yields
atmosphere and can never yield brick, wood grain, woven linen or hammered metal.

Recipes to add:

| Material | Technique |
|---|---|
| Wood grain | `feTurbulence` stretched one axis (`baseFrequency 0.02 0.4`) + `feColorMatrix` |
| Marble / granite | `type="fractalNoise"`, high `numOctaves`, hard contrast curve |
| Brick / tile / weave | `repeating-linear-gradient`, `conic-gradient` — no images |
| Crumpled paper, stucco, fabric | `feTurbulence` → `feDisplacementMap` on a flat fill |
| Rust / patina | turbulence → `feColorMatrix` → `feComposite`, masked to edges |
| Stone, cracked earth, cells | Worley/Voronoi on canvas |
| Ink bleed, letterpress | `feMorphology` |

**The headline technique: `feDiffuseLighting` / `feSpecularLighting` with turbulence as the
bump source.** Grain is flat; a real material has relief and a light direction. These two
filters are what make a surface look like something you could touch. Nothing in the
Toolroom uses them. This is the single highest-leverage addition available.

### 2. Fill REA and DEP

Counts are lopsided — TYP 10, GL 9, AMB/IMG/PLT 6, SYS/REV 5, but **REA 3 and DEP 3**.
Those two are exactly what make a page feel alive and expensive; they're thin because
they're hardest to author.

- **REA**: magnetic elements (asked for repeatedly, still missing), cursor state/label swap,
  click ripple, lens/magnifier, drag with inertia + rubber-band, real physics, hover-to-play video
- **DEP**: depth-of-field on scroll, volumetric light, a shadow that responds to a light
  position, layered translucency, perspective grid

### 3. Cheap and disproportionately impressive — take early

- **Scroll-scrubbed image sequence** (the Apple product spin). Absent entirely.
- **`mix-blend-mode: difference`** on a fixed nav or cursor so it auto-inverts over any
  background. Zero cost, very high impact.

### 4. Everything else from the research pass

Scroll: pinned section with changing content, horizontal scroll, elastic grid scroll,
progress indicators. Blend: text as mask over video, halftone/risograph/CMYK misregistration.
Type: `textPath`, circular text, split-flap, long shadow, optical-size and slant axes.
Reveal: staggered grid, SVG line drawing, blob-mask, curtain, page-transition overlays.
GL: **matcap** (best realism-per-millisecond), fresnel rim light, normal maps, bloom/DOF/SSR,
cloth, instanced geometry, 3D text. Ambient: volumetric fog, light leaks, rain on glass,
a breathing vignette.

### 5. The per-client living document

Approved in principle, deliberately NOT built inside the Toolroom (that would violate BLD
07's warning about a graveyard of stale rules). One per client, in the client's own folder.
Its highest-value part is a **decisions log** — *tried X, client said Y, landed on Z,
because W* — which nothing can recover after the fact. Earth Coffee's first entry already
exists: *reveal for large text/photo = blur-focus, NOT char-stagger, NOT line-mask, NOT
velocity-skew — all three built and discarded.*

---

## Standing rules that came out of this work

- **Show, never send.** Every version is a link they reload. A file only on request, after
  approval. The word "download" does not appear in a reply.
- **If you find a bug, fix it. Don't report it.**
- **Never fabricate.** No invented handle, price, testimonial or phone number.
- **Preserve what's already good; elevate only what is not.**
- **`element.click()` is not a click**, and a test that never ran looks identical to one
  that passed unless `elementFromPoint` confirms the target.
- **The catalogue is a vocabulary, not a spec.** If someone changes which named effect they
  want on the same element twice, stop matching names and ask what it should feel like.
- **Audit the architecture before tuning a number.**
- **A freshness warning applies to you too.**
