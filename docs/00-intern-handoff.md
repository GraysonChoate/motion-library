# Intern Handoff — Website Elevation Workflow

**Read this first. It is the entry point to everything else in this folder.**

> ⚠️ **Status: unvalidated, v1.** The research half (phases 1–6) has been run once
> against a real client. **The build half has never been run.** Nobody has taken
> research from this process through to a finished page, so there is no evidence yet
> that it produces better work than taste would have. Treat it as a hypothesis you
> are helping test — see [§8](#8-what-to-send-back).

---

## 1. What we actually do

We take a small business with a real identity and a website that undersells it,
and we **elevate the execution without rebranding the company**.

The premise, in one line:

> **We don't touch the brand. We light it.**

Almost every local business we look at already owns everything needed — a real
origin story, a distinctive product, colors, a vocabulary, a tagline. It's usually
buried under promo bars and product grids. Our job is to find what they own, move
it to the front, and give it motion and dimension.

**What this is not:**
- Not a rebrand. Not new logos, not new palettes, not new names.
- Not a copywriting exercise. Their words are almost always better than ours.
- Not a template. If the output could belong to a different client, start over.

---

## 2. The workflow

Seven phases. **Do them in order.** Each has a gate — do not start the next phase
until the gate passes. Most of the damage in the test run came from skipping ahead.

Rough first-pass timings for a single-location café or studio:

| # | Phase | Time | Output |
|---|---|---|---|
| 1 | Access check | 10 min | a stated list of what you can and can't reach |
| 2 | First-party scrape | 30 min | their raw HTML/CSS on disk |
| 3 | Measure | 20 min | palette + brightness table, all tier A |
| 4 | Mine words & structure | 30 min | verbatim copy file, latent structure |
| 5 | Diagnosis | 15 min | **one sentence** |
| 6 | Direction | 45 min | constraints doc, no code |
| 7 | Build | varies | the page |

### Phase 1 — Access check

Before promising anything, find out what you can actually reach. One probe each.

**Gate:** you have written down, explicitly, which sources you reached and which
you did not. If a fetch was blocked, that is a finding to report — *not* something
to paper over with a search-engine summary.

> **The single worst failure in the test run:** describing research in a way that
> implied the site had been read, when every fetch had been blocked. Everything
> built downstream inherited that false premise. **Never say "I scraped it" until
> bytes are on disk.**

### Phase 2 — First-party scrape

A small business's own site almost never fights scrapers. Start there, always.

```bash
UA="Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 \
(KHTML, like Gecko) Chrome/126.0 Safari/537.36"
D="clientdomain.com"

curl -sL -A "$UA" "https://$D/" -o home.html -w "http=%{http_code} bytes=%{size_download}\n"
for p in pages/about pages/our-story pages/menu; do
  curl -sL -A "$UA" "https://$D/$p" -o "$(basename $p).html" -w "$p http=%{http_code}\n"
done
```

Then extract, in this order:

```bash
# what platform, what fonts, what colors
grep -oiE '(myshopify|cdn\.shopify|squarespace|wix|wp-content)' home.html | sort | uniq -c | sort -rn
grep -ohiE 'font-family:[^;}"]{0,80}' home.html | sort -u
grep -ohE '#[0-9a-fA-F]{6}\b' home.html | tr 'A-Z' 'a-z' | sort | uniq -c | sort -rn | head -25
# their IA and their image assets
grep -ohE 'href="/[a-z0-9/_.-]{0,50}"' home.html | sort -u
grep -ohE '(cdn/shop/files|/assets)/[A-Za-z0-9_%.-]{3,80}\.(jpg|jpeg|png|webp)' home.html | sort -u
```

**Always grep the font names for the word `Trial`.** Trial-licensed fonts running
in production is a real liability, and worth raising.

**Gate:** HTML is on disk with a 200 and a non-trivial byte count.

### Phase 3 — Measure the palette

**Never eyeball a color. Measure it.** Two sources, both required.

**UI palette** — hex frequency in their HTML. Frequency ranks importance: the
most-repeated hex is the brand color.

**Photographic palette** — from their own photos:

```bash
for f in hero.jpg store1.jpg store2.jpg; do
  curl -sL -A "$UA" "https://$D/path/$f" -o "img_$f"
  echo "=== $f brightness=$(convert "img_$f" -colorspace Gray -format '%[fx:int(mean*100)]' info:)% ==="
  convert "img_$f" -resize 140x140! -colors 8 -depth 8 -format %c histogram:info: \
    | sed 's/^ *//' | sort -rn | head -8
done
```

**Mean brightness is a design directive, not a mood.** the test client's rooms measured
31–50%, so a dark page is *faithful to them*. If a client's rooms measure 80%, a
dark page is a costume you put on them.

⚠️ **Sanity-check every image before you measure it.** In the test run an image
search returned industrial V-belt product photos; the palette math ran perfectly and
produced a completely fictitious brand palette. Confirm the image actually depicts
the client — by filename, source domain, or dimensions — or throw it out.
**Correct arithmetic on wrong inputs is more dangerous than an error, because
nothing looks broken.**

**Gate:** a palette table where every hex traces to a measured source.

### Phase 4 — Mine their words and structure

The client is usually a better writer than the brief. Look for, in order:

1. **A latent narrative structure.** on the one client run so far, the story page already
   carried a named three-act arc — a complete scroll spine, sitting two clicks deep
   behind the homepage. **Never invent an arc before checking for theirs.**
2. **A tagline they already own.**
3. **Their best sentence.** Usually on an About page nobody links to.
4. **A naming system.** If every product in a range shares a theme, **that naming
   system is the art direction** — already decided, by them.
5. **A latent interaction.** A mix, grade, strength, or tier the client already
   exposes to customers is a signature interaction they named before you arrived.
6. **Trademarks and legal marks** — carry the ®.

**Gate:** a file of verbatim quotes with the page each came from.

### Phase 5 — Diagnosis

List what the homepage leads with. List their strongest owned material. **The gap is
the thesis.** Write it as one sentence.

From the one run so far:

> **The homepage is a coupon. The story is in the basement.**

**Gate:** one sentence. If it needs a paragraph, you don't have it yet.

### Phase 6 — Direction

Constraints first, all derived from measured data — palette from Phase 3, brightness
target from Phase 3, structure from Phase 4, copy from Phase 4. Then commit to **one**
direction and **one** signature interaction.

**Ban imported mood.** Reference sites carry a genre along with their technique. Steal
the mechanics — scroll-scrub, blur-stagger, mask wipe, mouse parallax — and reject the
genre. In the test run the references were all cold neural-tech product launches;
applied literally to a coffee brand you get *"an AI startup that happens to sell lattes."*

**Gate:** written direction with zero code, and every claim traceable to Phase 3 or 4.

### Phase 7 — Build

See [`02-technique-reference.md`](02-technique-reference.md) and open
`motion-bench.html`. Non-negotiables in [§6](#6-the-quality-floor).

---

## 3. Evidence tiers — tag every fact

This is the discipline that prevents the most expensive mistakes. Label every claim:

| Tier | Source | Use it? |
|---|---|---|
| **A — Measured** | bytes you downloaded and parsed | build on it |
| **B — Verbatim** | their own copy, quoted exactly | build on it |
| **C — Human-verified** | a screenshot or statement from a person | build on it |
| **D — Search summary** | third-party paraphrase | corroborate before using |
| **E — Inference** | reasoned from A or B | flag it as an inference |
| **F — Imagination** | your mental model of the brand | **never ship** |

**The cautionary pair from the test run:** an *inference* that the site was Shopify —
reasoned from `/collections/` and `/products/` URL patterns — was correct. A *guess*
that the brand was navy survived three rounds of discussion before measurement killed
it. Gold `#E3B245` was dominant the whole time, and the cool axis was slate-blue and
teal. Nothing built on that guess would have been theirs.

**Mixing tiers is how a guess becomes a build spec.** Say the tier out loud.

---

## 4. Tool reality — route by source type

Automation and humans have different reach. This table is the biggest time-saver here.

| Source | Automated fetch | Route it to |
|---|---|---|
| Client's own site | ✅ reliable | you, scripted |
| Client's CDN images | ✅ reliable | you + ImageMagick |
| Google / Bing / DuckDuckGo | ❌ shells, bot checks, junk | **a human's browser** |
| Instagram / TikTok / Facebook | ❌ 429 / 400 / empty JS | **a human's browser** |
| Yelp / TripAdvisor / press | ⚠️ varies | try once, then search |

**Rule: two failures on one source means switch source, not technique.** The test run
burned four attempts on Instagram — profile, API, embed, headless browser — when the
answer was one screenshot from a person. That isn't laziness; a real browser has a
residential IP and a logged-in session, and automation has neither.

**So ask for the human-only inputs in your first message, batched:**
1. Screenshot of Google Images for `"<brand>" interior`
2. Screenshot of the Instagram grid — nine tiles gives you their whole social voice
3. Screenshot of the homepage as they see it
4. Any brand assets they hold — logo files, brand guide

**Why IG matters for this client type:** for cafés, studios, gyms, and salons, the
brand lives on Instagram far more than on the website. Skipping it means missing the
actual identity. Ask early.

---

## 5. Known failure modes

Every one of these happened in the test run. They are cheap to repeat.

1. **Claiming a fetch succeeded when it was blocked.** Poisons everything downstream.
2. **Shipping a tier-F guess.** The navy call.
3. **Measuring an unverified image.** The V-belt palette.
4. **Trying one blocked source four ways** instead of switching sources.
5. **Generating paid assets with no visual reference.** Two video clips were generated
   from a text description with no reference attached, producing generic stock fire and
   cream that could belong to any coffee brand on earth. ~65 credits.
6. **Not confirming the medium first.** Those clips were generated one message before
   video was ruled out entirely. **Ask what the deliverable permits before spending.**
7. **Importing a reference's mood along with its mechanics.**
8. **Shipping demo-amplitude motion.** See below.

---

## 6. The quality floor

**Demo values ≠ ship values.** Everything in `motion-bench.html` is cranked so the
effect is obvious at a glance. Production wants the opposite: the page feels alive and
**the reader never notices the mechanism.** Ship values run roughly 40–50% of demo
values — full table in [`02-technique-reference.md`](02-technique-reference.md).

> **If a colleague can describe what the animation did, it's too strong.**

**Architecture — copy this before you copy any effect:**
one `requestAnimationFrame` loop for the whole page, every animated section registered
with an `IntersectionObserver` so nothing off screen computes. Eleven private loops
will idle a page at 100% CPU.

**Depth ≠ arrival.** Things fading in on scroll is not dimension. Parallax only reads
when **all three** are true: silhouettes that occlude each other, enough travel, and
blur on the nearest plane. Two out of three looks flat.

**Accessibility, non-negotiable:**
1. `prefers-reduced-motion` fallback on every effect
2. `aria-label` on any split text — splitting destroys the accessible string
3. `will-change` on anything animating `mask-image`, `clip-path`, or `filter`
4. Visible `:focus-visible` on every control
5. Clamp inputs **before** mapping, never outputs after
6. Re-check axis-dependent effects on mobile — a horizontal wipe on a one-column phone
   layout reveals nothing

---

## 7. Legal and ethical floor

Most of what we make starts as **unsolicited concept work**. That's a normal, respected
practice — and it has rules.

1. **Label it in the page.** A visible, persistent marker: unofficial concept study,
   not affiliated with the company. Nobody landing on the link should be able to
   mistake it for the real site.
2. **Invent nothing.** No prices, reviews, testimonials, classes, credentials, claims,
   or links that you did not verify. Tier A–C only.
3. **Respect marks.** Registered trademarks carry their ®.
4. **Use their real links.** Verify them; don't guess a URL pattern.
5. **Never present it as commissioned** or imply a relationship that doesn't exist.

---

## 8. What to send back

Because this workflow is unproven, your friction is data. When you finish a client,
report:

- **Where the phase gates were wrong** — too slow, too strict, in the wrong order
- **Anything in §4 that has changed** — platforms adjust their blocking constantly
- **Ship values you had to retune**, and for what kind of content
- **Failure modes not in §5** — add them
- **How long each phase actually took** versus the table in §2

Open a PR against this folder. The docs are the product as much as the code is.

---

## 9. Where everything lives

| File | What it's for |
|---|---|
| `00-intern-handoff.md` | this document — start here |
| `01-research-playbook.md` | the research process in full detail |
| `02-technique-reference.md` | code index + **demo-vs-ship dial table** |
| `../templates/research-card.md` | the fill-in research deliverable |
| `../motion-bench.html` | **open in a browser** — 11 live techniques |

**Your first day:** open `motion-bench.html` and move your cursor through every stage.
Then read `01` and fill a research card for any local business you like — a café you
know, your gym. Doing it once on a business you already understand is the fastest way
to see what the card catches that intuition misses.
